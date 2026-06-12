### Null Values

Why I Would Remove Them

Dataset is huge
Missing rows are tiny
Easier explanation
Cleaner feature engineering

Missing Completely At Random (MCAR)
Some timestamps accidentally not recorded.

Missing At Random (MAR)
Certain regions fail to report timestamps.

Missing Not At Random (MNAR)
Approval timestamp missing because approval never happened.
Null itself carries information.

If missing >10%:
Option 1:
Create missing flag
df['approval_missing'] = (
    df['order_approved_at'].isna()
).astype(int)

Option 2
Impute
median_timestamp

Option 3
Remove only if business logic says row is unusable.

Real Rule Used in Industry
<5% → drop
5-20% → impute
>30% → consider dropping column