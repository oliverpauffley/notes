- Last Billed Date based on `guddate` in `gusedom` where `guniquesys = gmulastbilled`from `gas`
- `gcustaccountno` links to `custaccountno` in `gas` and `customer`
- Total Used is `clibudgetusage` from `cli`
- Total Paid is `clibudgettotalpd` from `cli`
- AQ is `gaqkwh` or `GAQkWhRegs` from `gas` **only use gawkwh for single register sites**
- Unit rate is 
- Standing charge is 

- duel fuel discount = `3.392` if
	- `cus.custserviceLvl = EDF` and `cli.CLIServiceLvl in (UF, UG, UE, UJ)` and `cli.CLIServiceLvl not MXD`.

- Next BP review date = `max(clilivedate,clibudgetstart,clicpsdate)` plus x years where x is the minimum number to make this date today or later.
- Offtake from `ecofftake`.
- Currently monthly payment is `clibudgetamount` from `cli`

### Calculation
```sql
select
 cus.custaccountno,
 gus.guddate,
 gas.glastbilledgmu,
 gas.gaqkwh,
 gas.gaqkwhregs 
from customer as cus
left join gas on cus.custaccountno = gas.gcustaccountno 
left join gusedom as gus on gus.guduniquesys = gas.glastbilledgmu 
where cus.custaccountno = '3016818';
```
