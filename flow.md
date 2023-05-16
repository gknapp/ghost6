# Ghost 6 stock extruder & hot-end performance

Tests conducted using Eryone orange PLA (1.75mm).

I used a [flow test generator](https://hotend-flow-tester.netlify.app/) to produce Gcode requesting a range of flow rates 
across three printing temperatures: 200˚C, 210˚C and 220˚C.

This is replicates method used by [CNC Kitchen](https://www.youtube.com/watch?v=0xRtypDjNvI), 
weighing the extruded PLA and comparing it to the requested flow rate in mm<sup>3</sup>/s.

![Grid of flow rate tests on the Ghost 6 build surface](images/flow_test.jpg)

Flow rate requested and weight extruded (g) using a brass 0.4mm nozzle.

| Temp | 6 | 8 | 10 | 12 | 14 | 16 | 18 | 20 | 22 | 24 | 26 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 200 | 0.6 | 0.6 | 0.58 | 0.56 | 0.57 | 0.51 | 0.47 | 0.4 | 0.39 | 0.36 | 0.34 |
| 210 | 0.6 | 0.6 | 0.57 | 0.58 | 0.58 | 0.56 | 0.53 | 0.46 | 0.43 | 0.39 | 0.37 |
| 220 | 0.6 | 0.58 | 0.59 | 0.59 | 0.56 | 0.58 | 0.57 | 0.51 | 0.45 | 0.42 | 0.39 |

Taking 0.6g as the maximum and dividing all test results into this, we 
can see the relative flow rate (under) performance.

| Temp | 6 | 8 | 10 | 12 | 14 | 16 | 18 | 20 | 22 | 24 | 26 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 200 | 100.00 | 100.00 | 96.67 | 93.33 | 95.00 | 85.00 | 78.33 | 66.67 | 65.00 | 60.00 | 56.67 |
| 210 | 100.00 | 100.00 | 95.00 | 96.67 | 96.67 | 93.33 | 88.33 | 76.67 | 71.67 | 65.00 | 61.67 |
| 220 | 100.00 | 96.67 | 98.33 | 98.33 | 93.33 | 96.67 | 95.00 | 85.00 | 75.00 | 70.00 | 65.00 |

![Line chart of data in the table above, flow rate requested versus actual](images/flow_chart.png)