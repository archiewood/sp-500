# S&P 500

This page shows the daily close prices of selected companies in the S&P 500 index.

```sql companies
SELECT
  Symbol,
  Shortname
FROM sp500.joined_select
group by all
```

<Dropdown 
  data={companies} 
  name=company 
  value=Symbol
  label=Shortname
  multiple
  defaultValue={['AAPL', 'MSFT', 'GOOG']}
/>

```sql stocks
SELECT 
  Date,
  Symbol,
  Close,
  Shortname
from sp500.joined_select
where Symbol in ${inputs.company.value}
and Date > '2020-01-01'
```


<LineChart
  data={stocks}
  x=Date
  y=Close
  yFmt=usd
  series=Shortname
  yAxisTitle=Price
  title="S&P 500 Daily Close Prices"
/>