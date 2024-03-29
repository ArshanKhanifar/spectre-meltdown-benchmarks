# IBRS AKA Spectre Mitigation Benchmark
## Results of `syscall_timing`:

### Case 1:
This is from revision `9c0b808`, prior to the spectre patch.
```
test    loop    time    iterations      periteration
getppid 0       1.056983718     1643954 0.000000642
getppid 1       1.062569351     1652338 0.000000643
getppid 2       1.062568489     1651884 0.000000643
getppid 3       1.012717111     1577739 0.000000641
getppid 4       1.013082384     1575011 0.000000643
getppid 5       1.009982565     1573820 0.000000641
getppid 6       1.062569852     1651568 0.000000643
getppid 7       1.010441247     1568821 0.000000644
getppid 8       1.000173254     1558233 0.000000641
getppid 9       1.000189159     1554602 0.000000643
```

### Case 2:
This is after Spectre mitigation, but with no microcode update, and the feature disabled.

```
Clock resolution: 0.000000001
test    loop    time    iterations      periteration
getppid 0       1.006870203     1556529 0.000000646
getppid 1       1.004325684     1550679 0.000000647
getppid 2       1.012456539     1564780 0.000000647
getppid 3       1.007322553     1555973 0.000000647
getppid 4       1.049585085     1622360 0.000000646
getppid 5       1.002222293     1552266 0.000000645
getppid 6       1.059976170     1638160 0.000000647
getppid 7       1.059983320     1638311 0.000000646
getppid 8       1.049000106     1621577 0.000000646
getppid 9       1.054971295     1630598 0.000000646
```

### Case 3: 
This is after spectre mitigation, with microcode update, and with the feature disabled.
```
Clock resolution: 0.000000001
test    loop    time    iterations      periteration
getppid 0       1.061973972     1514845 0.000000701
getppid 1       1.061994821     1515481 0.000000700
getppid 2       1.062029075     1517938 0.000000699
getppid 3       1.060097689     1511387 0.000000701
getppid 4       1.055880843     1504905 0.000000701
getppid 5       1.059910822     1515130 0.000000699
getppid 6       1.039408527     1479926 0.000000702
getppid 7       1.034358214     1475908 0.000000700
getppid 8       1.062177534     1515115 0.000000701
getppid 9       1.061985292     1514728 0.000000701
```

### Case 4: 
After Spectre patch, microcode updated, and feature enabled:
```
Clock resolution: 0.000000001
test    loop    time    iterations      periteration
getppid 0       1.061977371     404051  0.000002628
getppid 1       1.061976308     404089  0.000002628
getppid 2       1.049032262     399124  0.000002628
getppid 3       1.062629659     404233  0.000002628
getppid 4       1.053453572     400804  0.000002628
getppid 5       1.062630859     404148  0.000002629
getppid 6       1.025238506     389524  0.000002632
getppid 7       1.062628436     404392  0.000002627
getppid 8       1.062637164     404177  0.000002629
getppid 9       1.062332443     404206  0.000002628
```

## Results of `buildworld`:
There were only two cases tested here, which had the conditions as the last two cases above.

### Case 1: 
This is with the feature disabled:
```
3172.08 real     94669.71 user      5003.62 sys
3159.38 real     94425.50 user      5024.42 sys
3164.79 real     94337.67 user      4996.08 sys
```

### Case 2:
This is with the feature enabled:
```
5440.64 real    106885.01 user      8030.31 sys
5403.62 real    106881.20 user      8092.97 sys 
5402.19 real    106827.67 user      8080.27 sys
```

## Statistics:
### syscall_timing: 
```
    N           Min           Max        Median           Avg        Stddev
x  10      6.41e-07      6.44e-07      6.43e-07     6.424e-07 1.0749677e-09
+  10      6.45e-07      6.47e-07      6.46e-07     6.463e-07 6.7494856e-10
Difference at 95.0% confidence
        3.9e-09 +/- 8.43313e-10
        0.607098% +/- 0.131847%
        (Student's t, pooled s = 8.97527e-10)
*  10      6.99e-07      7.02e-07      7.01e-07     7.005e-07 9.7182532e-10
Difference at 95.0% confidence
        5.81e-08 +/- 9.62799e-10
        9.04421% +/- 0.157479%
        (Student's t, pooled s = 1.0247e-09)
%  10     2.627e-06     2.632e-06     2.628e-06    2.6285e-06 1.3540064e-09
Difference at 95.0% confidence
        1.9861e-06 +/- 1.14863e-09
        309.169% +/- 0.475969%
        (Student's t, pooled s = 1.22247e-09)
```
### buildworld: 

#### real:

```
    N           Min           Max        Median           Avg        Stddev
x   3       3159.38       3172.08       3164.79     3165.4167     6.3731494
+   3       5402.19       5440.64       5403.62     5415.4833     21.798042
Difference at 95.0% confidence
        2250.07 +/- 36.3988
        71.0828% +/- 1.23406%
        (Student's t, pooled s = 16.0588)
```

#### user:

```
    N           Min           Max        Median           Avg        Stddev
x   3      94337.67      94669.71       94425.5     94477.627     172.04805
+   3     106827.67     106885.01      106881.2     106864.63     32.062056
Difference at 95.0% confidence
        12387 +/- 280.493
        13.111% +/- 0.33458%
        (Student's t, pooled s = 123.751)
```

#### sys:

```
    N           Min           Max        Median           Avg        Stddev
x   3       4996.08       5024.42       5003.62       5008.04     14.677915
+   3       8030.31       8092.97       8080.27       8067.85     33.124933
Difference at 95.0% confidence
        3059.81 +/- 58.0687
        61.098% +/- 1.30248%
        (Student's t, pooled s = 25.6194)
```

# PTI-PCID Benchmark

This repo contains the results of benchmarking multiple tasks on FreeBSD 12 with the PTI mitigation and Spectre mitigation.

## Results of `buildworld`:

### PTI=enabled, PCID=enabled

Mode | Time 1 | Time 2 | Time 3 | Average
--- | --- | --- | --- | --- 
real | 1695.96 | 1688.69 | 1701.44 | 1695.36 
user | 50535.65 | 50380.41 | 50342.40 | 50419.49
sys | 2730.79 | 2710.22 | 2733.57 | 2724.86

### PTI=disabled, PCID=enabled

Mode | Time 1 | Time 2 | Time 3 | Average
--- | --- | --- | --- | ---
real | 1712.18 | 1677.08 | 1691.40 | 1693.55 
user | 50409.49 | 50223.23 | 50273.89 | 50302.2
sys | 2623.50 | 2652.31 | 2658.68 | 2644.83

### PTI=enabled, PCID=disabled

Mode | Time 1 | Time 2 | Time 3 | Average
--- | --- | --- | --- | ---
real | 1703.57 | 1705.30 | 1729.55 | 1712.81 
user | 50781.66 | 50754.05 | 50842.26 | 50792.66
sys | 2740.31 | 2772.59 | 2787.22 | 2766.71

### PTI=disabled, PCID=enabled

Mode | Time 1 | Time 2 | Time 3 | Average
--- | --- | --- | --- | ---
real | 1706.72 | 1697.84 | 1686.90 | 1697.15 
user | 50401.75 | 50230.85 | 50226.37 | 50286.32
sys | 2637.55 | 2620.79 | 2654.58 | 2637.64

## Results of `syscall_timing getppid`

### PTI=enabled, PCID=enabled
```
Clock resolution: 0.000000001
test    loop    time    iterations      periteration
getppid 0       1.062550426     3119652 0.000000340
getppid 1       1.062600549     3783239 0.000000280
getppid 2       1.062599129     4043920 0.000000262
getppid 3       1.062550845     4041808 0.000000262
getppid 4       1.062600487     4043318 0.000000262
getppid 5       1.022923818     3891769 0.000000262
getppid 6       1.062551825     4043494 0.000000262
getppid 7       1.037910806     3944886 0.000000263
getppid 8       1.062548954     4042458 0.000000262
getppid 9       1.062553298     4043984 0.000000262
```

### PTI=enabled, PCID=disabled
```
Clock resolution: 0.000000001
test    loop    time    iterations      periteration
getppid 0       1.062550179     2274210 0.000000467
getppid 1       1.062549186     2721737 0.000000390
getppid 2       1.062550267     3088463 0.000000344
getppid 3       1.062547916     3102510 0.000000342
getppid 4       1.016532138     2965114 0.000000342
getppid 5       1.012793858     2955245 0.000000342
getppid 6       1.059916867     3094867 0.000000342
getppid 7       1.060025231     3094446 0.000000342
getppid 8       1.059906532     3090372 0.000000342
getppid 9       1.055016940     3078349 0.000000342
```

### PTI=disabled, PCID=enabled
```
Clock resolution: 0.000000001
test    loop    time    iterations      periteration
getppid 0       1.050982283     6858863 0.000000153
getppid 1       1.059966019     8387507 0.000000126
getppid 2       1.059972267     8954311 0.000000118
getppid 3       1.059969986     8952248 0.000000118
getppid 4       1.059984758     8954050 0.000000118
getppid 5       1.025501889     8662441 0.000000118
getppid 6       1.062598583     8976668 0.000000118
getppid 7       1.036027999     8739264 0.000000118
getppid 8       1.061528280     8965968 0.000000118
getppid 9       1.061915689     8970430 0.000000118
```

### PTI=disabled, PCID=disabled
```
Clock resolution: 0.000000001
test    loop    time    iterations      periteration
getppid 0       1.062599742     6960416 0.000000152
getppid 1       1.062550606     8469589 0.000000125
getppid 2       1.062595174     8923683 0.000000119
getppid 3       1.062550032     8923558 0.000000119
getppid 4       1.062549608     8920523 0.000000119
getppid 5       1.020479393     8556939 0.000000119
getppid 6       1.062549724     8922860 0.000000119
getppid 7       1.062551476     8922805 0.000000119
getppid 8       1.062600428     8924624 0.000000119
getppid 9       1.062549309     8922057 0.000000119
```


