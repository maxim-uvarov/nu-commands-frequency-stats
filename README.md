<h1 align="center">nu-history-tools</h1>
<h3 align="center">Nushell🚀 module for commands history analytics</h3>

A Nushell module to analyze the command frequencies in Nushell history, generate cool graphs, benchmark statistics with other users, and generate a file with statistics to share with the community.

Aggregated results, produced by the `aggregate-submissions` command can be found in the [csv file](https://github.com/nushell-prophet/nu-history-tools/tree/main/assets/script_results/aggregated-submissions.csv)

The history of nushell commands by releases can be found in [this csv](https://github.com/nushell-prophet/nu-history-tools/blob/main/assets/crates_parsing/cmds_by_crates_and_tags.csv)

![nu-history-tools2](https://github.com/nushell-prophet/nu-history-tools/assets/4896754/5053ede0-d53a-46be-bd71-7f066eca7025)

## Installation

```nushell no-run
> git clone https://github.com/nushell-prophet/nu-history-tools; cd nu-history-tools
```

## Analyze your stats and benchmark them with other users' submissions.

The output of `analyze-history` contains a lot of informational messages (as you can see in the next block).
These informational messages can be silenced using the `--quiet` flag.

```nushell
> use nu-history-tools; let $res = nu-history-tools analyze-history; $res | first 10
*******************************************************************************
                        nu-commands-frequency-stats v2.1
*******************************************************************************

Your history is in sqlite format and will be used for analysis. Additionally,
you have history in txt format, which consists of 496 lines. It will be used
for analysis as well.

Your stats have been saved to
/Users/user/git/nu-stats/stats_submissions/v2+WriteYourNick.csv. Please
consider donating them to the original repository
https://github.com/nushell-prophet/nu-history-tools/tree/main/stats_submissions
.

*******************************************************************************
                Aggregated stats of other users for benchmarks.
                   They will be displayed in the final table.
*******************************************************************************

freq_by_user (frequency norm by user) includes stats from all users. You can
pick some of them by providing the --pick_users flag: stats --pick_users or
aggregate-submissions --pick_users.

╭─#──┬──────user──────┬─command_entries─╮
│ 0  │ maximuvarov    │          120938 │
│ 1  │ vinlet         │           33817 │
│ 2  │ fdncred        │           18538 │
│ 3  │ nu_scripts     │           11214 │
│ 4  │ kubouch        │           10170 │
│ 5  │ ErichDonGubler │           10101 │
│ 6  │ chtenb         │            9376 │
│ 7  │ shinyzero0     │            9247 │
│ 8  │ dazfuller      │            7354 │
│ 9  │ cptpiepmatz    │            4199 │
│ 10 │ zjp            │            2764 │
│ 11 │ sholderbach    │            2114 │
│ 12 │ horasal        │            1373 │
│ 13 │ nu_std         │             985 │
│ 14 │ pingiun        │             894 │
│ 15 │ nicokosi       │             255 │
╰─#──┴──────user──────┴─command_entries─╯
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

╭─#─┬──name──┬──category──┬─freq─┬─freq_norm─┬─freq_norm_bar─┬──timeline───┬─importance─┬─importance_b─┬───freq_by_user───╮
│ 0 │ ls     │ filesystem │ 7368 │      1.00 │ ██████████    │ ▅█▆▆▅▆▆▇▆▃▁ │       1.00 │ ████████████ │ ▇▄█▁█▃▁█▄▄█▆█▁▆▇ │
│ 1 │ get    │ filters    │ 7341 │      1.00 │ ██████████    │ ▆█▆▅▅▄▃▃▃▃▁ │       0.83 │ ██████████   │ ▇█▅▂▆▂▁▄▃▁▂▃▂▃▂█ │
│ 2 │ open   │ filesystem │ 6278 │      0.85 │ ████████▌     │ ▄█▅▃▂▄▄▅▅▅▁ │       0.79 │ █████████▌   │ ▆█▄▁▄▂▁▄▃▆▂▃▃▁▂▇ │
│ 3 │ let    │ core       │ 4272 │      0.58 │ █████▊        │ ▇█▅▇▅▅▃▆▅▅▁ │       0.64 │ ███████▋     │ ▅▃▄█▃▁▁▂▁▁▂▂▂▆▃▁ │
│ 4 │ each   │ filters    │ 4093 │      0.56 │ █████▌        │ ▄█▆▇▆▅▄▇█▅▁ │       0.57 │ ██████▊      │ ▅█▃▂▄▂▁▂▁▁▂▃▂▂▁▁ │
│ 5 │ where  │ filters    │ 3648 │      0.50 │ █████         │ ▄█▄▅█▇▆▆▄▇▁ │       0.51 │ ██████▏      │ ▇█▅▂▅▂▁▃▃▂▂▅▃▃▁▁ │
│ 6 │ upsert │ filters    │ 2848 │      0.39 │ ███▉          │ ▅▅▄▄█▄▂▁▁▁▁ │       0.17 │ ██           │ █▅▃▂▁▁▁▁▁▁▁▁▁▁▁▁ │
│ 7 │ first  │ filters    │ 2404 │      0.33 │ ███▎          │ ▄█▅▃▅▃▃▃▃▂▁ │       0.27 │ ███▎         │ █▁▄▂▁▂▁▁▂▄▃▃▁▁▁▁ │
│ 8 │ polars │ dataframe  │ 2305 │      0.31 │ ███▏          │ ▁▁▁▁▁▁▁█▅▁▁ │       0.05 │ ▌            │ █▁▁▁▁▁▁▁▁▁▁▁▁▁▁▁ │
│ 9 │ lines  │ filters    │ 2031 │      0.28 │ ██▊           │ ▂▄▄▃▅▃▅▄▃█▁ │       0.45 │ █████▍       │ ██▆▂▆█▁▇▁▅▇▆▃▁▁▁ │
╰─#─┴──name──┴──category──┴─freq─┴─freq_norm─┴─freq_norm_bar─┴──timeline───┴─importance─┴─importance_b─┴───freq_by_user───╯
```

## Analyze submissions separately

```nushell
> use nu-history-tools; let $res2 = nu-history-tools aggregate-submissions --quiet; $res2 | first 5
╭─#─┬─name─┬──category──┬─freq_overall─┬─users_count─┬─f_n_per_user─┬───freq_by_user───┬─importance─┬─importance_b─╮
│ 0 │ ls   │ filesystem │        15045 │          14 │         0.62 │ ▇▄█▁█▃▁█▄▄█▆█▁▆▇ │       1.00 │ ████████████ │
│ 1 │ cd   │ filesystem │         8492 │          15 │         0.43 │ ▂▃▄▁▇▃▂▁██▇▄▄▁█▁ │       0.87 │ ██████████▍  │
│ 2 │ get  │ filters    │        13710 │          16 │         0.37 │ ▇█▅▂▆▂▁▄▃▁▂▃▂▃▂█ │       0.83 │ ██████████   │
│ 3 │ open │ filesystem │        12561 │          15 │         0.36 │ ▆█▄▁▄▂▁▄▃▆▂▃▃▁▂▇ │       0.79 │ █████████▌   │
│ 4 │ help │ core       │         3397 │          14 │         0.29 │ ▂▂▅▁▃▁▁▂▂▂▃█▁▁▇█ │       0.69 │ ████████▎    │
╰─#─┴─name─┴──category──┴─freq_overall─┴─users_count─┴─f_n_per_user─┴───freq_by_user───┴─importance─┴─importance_b─╯
```
