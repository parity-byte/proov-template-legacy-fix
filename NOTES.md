# What I checked, and what the agent got wrong

Write this yourself, in your own words. It is the part of the repo that proves the work is yours.

## What the agent got wrong
When generating the initial modernization pass and test suite, the agent made a logical error in the test assertion by expecting `due == 0` for `VOS-4471`, which is 99% worn and should be flagged as due. It also attempted to preserve flawed behaviors and required manual steering to ensure it properly removed dead code and didn't touch core rules.

## What I checked before I accepted its work
I manually inspected `km_wachter.py` and `settings.cfg` to confirm that `SERVICE_INTERVAL_KM = 15000` and `WARN_AT_PERCENT = 80` were untouched. I also reviewed the unit test cases directly, verified the floating-point division fix, and executed `python verify.py` locally to ensure all 11 evaluation checks turned green before committing.

## What the data actually said
The historical fleet data revealed that breakdown risk is heavily driven by `km_since_service`, which showed a 61% difference between broken and intact vehicles (climbing from a 3% breakdown rate in the bottom quartile to 57% in the top quartile). In contrast, intuitive assumptions like overall `odometer_km` (+0.3%) and `age_years` (-0.2%) provided virtually zero predictive signal.