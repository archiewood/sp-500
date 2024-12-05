# S&P 500

This page shows the daily close prices of selected companies in the S&P 500 index.

```sql companies
SELECT
  Symbol,
  Shortname
FROM sp500.joined_select
group by all
```

```sql dates
select 
  date
from sp500.joined_select
where Date > '2018-01-01'
group by all
```

<DateRange name=date_filter data={dates} dates=date defaultValue={'Year To Date'}/>

<Dropdown 
  data={companies} 
  name=company 
  value=Symbol
  label=Shortname
  multiple
  defaultValue={['AAPL', 'TSLA', 'GOOG']}
/>




```sql stocks
SELECT 
  Date,
  Symbol,
  Shortname,
  Close,
from sp500.joined_select
where Symbol in ${inputs.company.value}
and Date between '${inputs.date_filter.start}' and '${inputs.date_filter.end}'
and Date > '2018-01-01'
```

```sql total_records
select count(*) as records from ${stocks}
```


<LineChart
  data={stocks}
  x=Date
  y=Close
  yFmt=usd0
  series=Shortname
  yAxisTitle=Price
  legend
  title="S&P 500 Daily Close Prices"
/>

Total records: <Value data={total_records} column=records fmt=num/>