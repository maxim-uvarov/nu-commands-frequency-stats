<h1 align="center">nu-history-tools</h1>
<h3 align="center">Nushell🚀 module for commands history analytics</h3>

A Nushell module to analyze the command frequencies in Nushell history, generate cool graphs, benchmark statistics with other users, and generate a file with statistics to share with the community.

Aggregated results, produced by the `aggregate-submissions` command can be found in the [csv file](https://github.com/nushell-prophet/nu-history-tools/tree/main/script_results/aggregated-submissions.csv)

The history of nushell commands by releases can be found in [this csv](https://github.com/nushell-prophet/nu-history-tools/blob/main/crates_parsing/cmds_by_crates_and_tags.csv)

![nu-history-tools2](https://github.com/nushell-prophet/nu-history-tools/assets/4896754/5053ede0-d53a-46be-bd71-7f066eca7025)

## Installation

```nushell no-run
> git clone https://github.com/nushell-prophet/nu-history-tools; cd nu-history-tools
```

## Analyze your stats and benchmark them with other users' submissions.

```nushell
*******************************************************************************
> overlay use nuht.nu; let $res = nu-hist-stats; $res | first 10
                        nu-commands-frequency-stats v2.0
*******************************************************************************

Your history is in sqlite format and will be used for analysis. Additionally,
you have history in txt format, which consists of 306 entries. It will be
used for analysis as well.


This script was tested on [0.88.1]. You have 0.89.0. If you have problems
running this script, consider upgrading Nushell.

The script is calculating stats now. On an M1 Mac with a history of ~50,000
entries, It runs for about a minute. Please wait

Your stats have been saved to
/Users/user/git/nu-stats/stats_submissions/v2+WriteYourNick.csv. Please
consider donating them to the original repository
https://github.com/nushell-prophet/nu-history-tools/tree/main/stats_submissions.

*******************************************************************************
Aggregated stats of other users for benchmarks.
They will be displayed in the final table.
*******************************************************************************

freq_by_user (frequency norm by user) includes stats from all users. You can
pick some of them by providing the --pick_users flag: nu-hist-stats
--pick_users or aggregate-submissions --pick_users.

╭─#──┬──────user──────┬command_entries╮
│ 0  │ maximuvarov    │         79655 │
│ 1  │ vinlet         │         33817 │
│ 2  │ fdncred        │         18500 │
│ 3  │ kubouch        │         10170 │
│ 4  │ ErichDonGubler │         10101 │
│ 5  │ chtenb         │          9376 │
│ 6  │ shinyzero0     │          9247 │
│ 7  │ nu_scripts     │          8622 │
│ 8  │ dazfuller      │          7354 │
│ 9  │ cptpiepmatz    │          4199 │
│ 10 │ zjp            │          2764 │
│ 11 │ sholderbach    │          2114 │
│ 12 │ horasal        │          1373 │
│ 13 │ nu_std         │          1202 │
│ 14 │ pingiun        │           894 │
│ 15 │ nicokosi       │           255 │
╰────┴────────────────┴───────────────╯

*******************************************************************************
                                Resulting table
*******************************************************************************
A note about some columns:
- freq - indicates the overall frequency of use of the given command for the
currently analyzed source
- freq_norm - represents the overall frequency normalized
- freq_norm_bar - shows the overall frequency normalized in a bar chart format
- timeline - displays the dynamics, indicating when the command was used
throughout your history
- importance - calculated as the geometric mean of the number of users who
used this command and the average normalized frequency
- freq_by_user (frequency norm by user) - each bar in the sparkline column
represents one user (order is shown in the table above).

╭──name──┬──category──┬─freq─┬freq_norm┬freq_norm_bar┬────────────────timeline────────────────┬importance┬─importance_b─┬───freq_by_user───╮
│ ls     │ filesystem │ 5204 │    0.82 │ ████████▏   │ ▃▃▃▂▃▂▃▅█▅▃▃▅▃▃▄▄▂▃▆▄▂▂▃▂▃▃▂▃▄▅▂▃▁▃▅▃▃ │     1.00 │ ████████████ │ ▆▄██▃▁█▁▄▄█▆█▁▆▇ │
│ cd     │ filesystem │ 1101 │    0.17 │ █▊          │ ▃▅▆▅▅▂▇█▃▆▄▂▃▅▄▄▂▂▂▃▂▂▂▂▁▂▃▂▂▂▅▂▃▁▂▄▄▄ │     0.84 │ ██████████▏  │ ▂▃▄▇▃▂▁▁██▇▄▄▁█▁ │
│ get    │ filters    │ 6378 │       1 │ ██████████  │ ▂▂▂▃▃▆▄▄█▂▃▃▄▅▁▂▃▄▁▄▂▂▂▃▃▂▂▂▃▃▂▂▃▁▂▂▂▁ │     0.82 │ █████████▊   │ ██▅▆▂▁▄▂▃▁▂▃▂▃▂█ │
│ open   │ filesystem │ 4287 │    0.67 │ ██████▊     │ ▂▂▃▃▃▃▃▇█▄▃▂▅▆▂▂▂▃▂▃▂▂▂▂▂▂▂▁▃▂▄▄▂▁▂▅▃▃ │     0.79 │ █████████▌   │ ▆█▄▄▂▁▄▁▃▆▂▃▃▁▂▇ │
│ help   │ core       │  911 │    0.14 │ █▍          │ ▆███▄▂▃▄▂▂▂▂▂▃▄▂▁▃▅▂▃▁▁▃▂▂▂▁▁▁▁▁▁▁▁▂▁▁ │     0.67 │ ████████▏    │ ▂▂▅▃▁▁▂▁▂▂▃█▁▁▇█ │
│ let    │ core       │ 3306 │    0.52 │ █████▏      │ ▂▂▃▃▅▄▃▃▃▅▅▄▄▂▃▃▃▂▂▄▂▂▄█▅▃▃▂▂▃▅▃▃▁▃▃▂▂ │     0.62 │ ███████▌     │ ▅▃▄▃▁▁▂█▁▁▂▂▂▆▃▁ │
│ each   │ filters    │ 2772 │    0.43 │ ████▍       │ ▂▂▂▂▂▃▃▃▅▃▂▃▃█▁▁▁▂▃▅▂▃▄▃▂▃▃▂▃▂▄▂▃▁▃▃▂▂ │     0.54 │ ██████▌      │ ▄█▃▄▂▁▂▂▁▁▂▃▂▂▁▁ │
│ config │ env        │    9 │    0.00 │             │ ▁▁▁▆█▁▁▁▁▁▁▃▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁▃▁▁ │     0.49 │ █████▉       │ ▁▁▃█▁▁▅▁▁▂▆▂▂▁▆▅ │
│ where  │ filters    │ 2469 │    0.39 │ ███▉        │ ▂▂▂▁▃▃▅█▆▂▃▁▄▄▂▁▃▁▂▃▃▂▃▅▇▂▃▃▇▄▆▅▄▁▃▅▂▃ │     0.49 │ █████▉       │ ▆█▅▅▂▁▃▂▃▂▂▅▃▃▁▁ │
│ lines  │ filters    │ 1169 │    0.18 │ █▉          │ ▁▂▂▃▃▁▂▁▆▂▃▄▂▂▁▁▃█▃▂▃▄▃▁▆▂▆▃▃▁▅▂▂▁▁▃▅▅ │     0.43 │ █████▏       │ ▆█▆▆█▁▇▂▁▅▇▆▃▂▁▁ │
╰────────┴────────────┴──────┴─────────┴─────────────┴────────────────────────────────────────┴──────────┴──────────────┴──────────────────╯

```

## Analyze submissions separately

```nushell
> use nuht.nu aggregate-submissions; let $res2 = (aggregate-submissions); $res2 | first 5
*******************************************************************************
Aggregated stats of other users for benchmarks.
They will be displayed in the final table.
*******************************************************************************

freq_by_user (frequency norm by user) includes stats from all users. You can
pick some of them by providing the --pick_users flag: nu-hist-stats
--pick_users or aggregate-submissions --pick_users.

╭─#──┬──────user──────┬command_entries╮
│ 0  │ maximuvarov    │         79655 │
│ 1  │ vinlet         │         33817 │
│ 2  │ fdncred        │         18500 │
│ 3  │ kubouch        │         10170 │
│ 4  │ ErichDonGubler │         10101 │
│ 5  │ chtenb         │          9376 │
│ 6  │ shinyzero0     │          9247 │
│ 7  │ nu_scripts     │          8622 │
│ 8  │ dazfuller      │          7354 │
│ 9  │ cptpiepmatz    │          4199 │
│ 10 │ zjp            │          2764 │
│ 11 │ sholderbach    │          2114 │
│ 12 │ horasal        │          1373 │
│ 13 │ nu_std         │          1202 │
│ 14 │ pingiun        │           894 │
│ 15 │ nicokosi       │           255 │
╰────┴────────────────┴───────────────╯

╭─name─┬──category──┬freq_overall┬users_count┬f_n_per_user┬───freq_by_user───┬importance┬─importance_b─┬───crate────┬first_tag┬last_tag╮
│ ls   │ filesystem │      12467 │        15 │       0.61 │ ▆▄██▃▁█▁▄▄█▆█▁▆▇ │     1.00 │ ████████████ │ nu-command │ 0.2.0   │ 0.89.0 │
│ cd   │ filesystem │       7911 │        15 │       0.43 │ ▂▃▄▇▃▂▁▁██▇▄▄▁█▁ │     0.84 │ ██████████▏  │ nu-command │ 0.2.0   │ 0.89.0 │
│ get  │ filters    │      12461 │        16 │       0.38 │ ██▅▆▂▁▄▂▃▁▂▃▂▃▂█ │     0.82 │ █████████▊   │ nu-command │ 0.2.0   │ 0.89.0 │
│ open │ filesystem │      10290 │        16 │       0.36 │ ▆█▄▄▂▁▄▁▃▆▂▃▃▁▂▇ │     0.79 │ █████████▌   │ nu-command │ 0.2.0   │ 0.89.0 │
│ help │ core       │       3273 │        14 │       0.30 │ ▂▂▅▃▁▁▂▁▂▂▃█▁▁▇█ │     0.67 │ ████████▏    │ nu-command │ 0.3.0   │ 0.89.0 │
╰──────┴────────────┴────────────┴───────────┴────────────┴──────────────────┴──────────┴──────────────┴────────────┴─────────┴────────╯

> use nuht.nu [aggregate-submissions]; let $res = aggregate-submissions; $res | first 10
*******************************************************************************
Aggregated stats of other users for benchmarks.
They will be displayed in the final table.
*******************************************************************************

freq_by_user (frequency norm by user) includes stats from all users. You can
pick some of them by providing the --pick_users flag: nu-hist-stats
--pick_users or aggregate-submissions --pick_users.

╭─#──┬──────user──────┬command_entries╮
│ 0  │ maximuvarov    │         79655 │
│ 1  │ vinlet         │         33817 │
│ 2  │ fdncred        │         18500 │
│ 3  │ kubouch        │         10170 │
│ 4  │ ErichDonGubler │         10101 │
│ 5  │ chtenb         │          9376 │
│ 6  │ shinyzero0     │          9247 │
│ 7  │ nu_scripts     │          8622 │
│ 8  │ dazfuller      │          7354 │
│ 9  │ cptpiepmatz    │          4199 │
│ 10 │ zjp            │          2764 │
│ 11 │ sholderbach    │          2114 │
│ 12 │ horasal        │          1373 │
│ 13 │ nu_std         │          1202 │
│ 14 │ pingiun        │           894 │
│ 15 │ nicokosi       │           255 │
╰────┴────────────────┴───────────────╯

╭──name──┬──category──┬freq_overall┬users_count┬f_n_per_user┬───freq_by_user───┬importance┬─importance_b─┬────crate────┬first_tag┬last_tag╮
│ ls     │ filesystem │      12467 │        15 │       0.61 │ ▆▄██▃▁█▁▄▄█▆█▁▆▇ │     1.00 │ ████████████ │ nu-command  │ 0.2.0   │ 0.89.0 │
│ cd     │ filesystem │       7911 │        15 │       0.43 │ ▂▃▄▇▃▂▁▁██▇▄▄▁█▁ │     0.84 │ ██████████▏  │ nu-command  │ 0.2.0   │ 0.89.0 │
│ get    │ filters    │      12461 │        16 │       0.38 │ ██▅▆▂▁▄▂▃▁▂▃▂▃▂█ │     0.82 │ █████████▊   │ nu-command  │ 0.2.0   │ 0.89.0 │
│ open   │ filesystem │      10290 │        16 │       0.36 │ ▆█▄▄▂▁▄▁▃▆▂▃▃▁▂▇ │     0.79 │ █████████▌   │ nu-command  │ 0.2.0   │ 0.89.0 │
│ help   │ core       │       3273 │        14 │       0.30 │ ▂▂▅▃▁▁▂▁▂▂▃█▁▁▇█ │     0.67 │ ████████▏    │ nu-command  │ 0.3.0   │ 0.89.0 │
│ let    │ core       │       7308 │        14 │       0.25 │ ▅▃▄▃▁▁▂█▁▁▂▂▂▆▃▁ │     0.62 │ ███████▌     │ nu-cmd-lang │ 0.25.0  │ 0.89.0 │
│ each   │ filters    │       7376 │        14 │       0.19 │ ▄█▃▄▂▁▂▂▁▁▂▃▂▂▁▁ │     0.54 │ ██████▌      │ nu-command  │ 0.13.0  │ 0.89.0 │
│ config │ env        │       1587 │        14 │       0.16 │ ▁▁▃█▁▁▅▁▁▂▆▂▂▁▆▅ │     0.49 │ █████▉       │ nu-command  │ 0.2.0   │ 0.89.0 │
│ where  │ filters    │       5750 │        13 │       0.17 │ ▆█▅▅▂▁▃▂▃▂▂▅▃▃▁▁ │     0.49 │ █████▉       │ nu-command  │ 0.2.0   │ 0.89.0 │
│ lines  │ filters    │       3501 │        14 │       0.12 │ ▆█▆▆█▁▇▂▁▅▇▆▃▂▁▁ │     0.43 │ █████▏       │ nu-command  │ 0.2.0   │ 0.89.0 │
╰────────┴────────────┴────────────┴───────────┴────────────┴──────────────────┴──────────┴──────────────┴─────────────┴─────────┴────────╯

```
