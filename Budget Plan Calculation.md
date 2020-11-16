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
select distinct on (cli.clinumber)
	cus.custaccountno as cust_account_no,
	cli.clinumber as cli_number,
	gas.greference as g_reference1,
	cli.clibudgetusage as usage,
	cli.clibudgettotalpd as total_paid,
	gus.guddate as last_billed_date,
	gas.gaqkwh,
	gas.gaqkwhregs,
	pmd.pmdgasppkwh as gas_ppkwh,
	pmd.pmdgdppkwh as gd_ppkwh,
	pmd.pmdstorageppkwh as storage_ppkwh ,
	pmd.pmde7dayppkwh as de_7_day_ppkwh,
	pmd.pmde7nightppkwh as de_7_night_ppkwh,
	pmd.pmdgasdaily as gas_daily ,
	pmd.pmdgddaily as gd_daily ,
	pmd.pmde7daily as de_7_daily,
	pes.pmdateto,
	cus.custservicelvl as cust_service_level,
	cli.cliservicelvl as cli_service_level,
	cli.clilivedate as live_date,
	cli.clibudgetstart as budget_start,
	cli.clicpsdate as cps_date,
	cli.clibudgetamount as budget_amount
from
	customer as cus
join cli on
	cus."_eq_logic_id" = cli."_eq_parent_logic_id" and cli.cliservicelvl like '%OPB%'
join gas on
	cus.custaccountno = gas.gcustaccountno
join gusedom as gus on
	gus.guduniquesys = gas.glastbilledgmu
join pesmast as pes on
	gus.gudtariff = pes.pmtariff
join pmdetail as pmd on
	pes."_eq_logic_id" = pmd."_eq_parent_logic_id" and gas.gregion = pmd.pmdregion 
where
	cus.custaccountno = '3142263'
order by
	cli.clinumber,
	pes.pmdateto ;

```
