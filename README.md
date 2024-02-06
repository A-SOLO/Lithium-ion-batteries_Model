Lithium-ion batteries are becoming ubiquitous in our lives, from consumer electronics to EVs. Here, we will work on time series data of these batteries in two different situations consisting two parts - Part 1 & Part 2.

# Part 1 - Feature extraction
### Definitions:
1. SOC (State Of Charge) : It is the level of charge in a battery relative to its capacity. A
battery is fully charged when it is at 100% SOC and fully discharged when it is at 0% SOC.
2. FEC (Full Equivalent Cycles) : FEC can be defined as the number of full charge-discharge
cycles that a battery has undergone. When a battery gets charged from 20% SOC to 70%
SOC and then discharged back to 20% SOC, its FEC does not increase by 1. Instead, it takes
two such “half” cycles for the FEC to go up by 1. This is because the FEC is measured
based on the charge throughput of the battery; it increases by unity only when the entire
capacity of the battery gets drained from it and then pumped back in again regardless of the
number of steps.

### Description of the [dataset1](https://github.com/A-SOLO/LOHUM_PS_file/blob/main/Part1.csv):
1. There are 4 features : timestamp, soc, voltage, current.
2. The units of voltage and current are Volts and Amperes respectively.

### Tasks:
1. Perform __data preprocessing__ - remove null values, look for outliers and clean up the data.
2. Based on SOC and current, __create an algorithm to obtain the FECs__ that the given battery
has undergone. Present the obtained FEC along with your reasoning in the write up section.
Please note that the 'current' column does not discriminate between charging current and
discharging current. (hint : add a new feature – ‘charge current’ by monitoring the change in
SOC).
3. The capacity of a battery is measured in Ampere hours (Ah). Is it possible to obtain the
capacity of the battery from the given information? If yes, __calculate the capacity of the
battery__ as an average over the first ten cycles.


# Part 2 - Regression
### Definitions:
1. RUL (Remaining Useful Life) : The capacity of a battery fades over time and cycles due to
various degradation mechanisms that occur within it. Typically, a battery is retired from use
when its capacity drops below 80% of its original capacity. At a given point during its
lifetime, the remaining number of cycles that can be extracted from the battery can be
regarded as the RUL of the battery.
2. SOH (State Of Health) : It is the ratio of a battery’s present capacity to its initial capacity.
SOH = current capacity/initial capacity.

### Description of the [dataset2](https://github.com/A-SOLO/LOHUM_PS_file/blob/main/Part2.csv.xlsx):
1. The dataset consists of two columns : Cycle_Index, Discharge_Capacity (Ah)
2. Cycle_Index represents the FEC count of the battery and Discharge_Capacity (Ah) is the
capacity measured while discharging the battery from 100% SOC to 0%.

### Tasks:
1. __Model the SOH__ of the cell as a function of cycle number.
   * Explain the model clearly in the write-up section.
   * Describe how the code ran on the dataset: parameters used, time taken etc.
   * Present the model as a function named 'Predict_SOH' that takes a pandas dataframe with the same column names as the provided dataset as the argument and returns SOH values as an array. Define the function as follows:

                               def Predict_SOH(dataframe)  
                               .....  
                               return [SOH]
3. Using the model, __determine the RUL of the battery__ at 500, 1000, 2000, 3000 and 3500 cycles.
   Plot the predicted values and the actual values and add this plot with proper title and legend to the write-up section. Assume that 80% SOH indicates that the battery has reached its end of life.
5. Write a __function to evaluate the performance of the model__, named 'Estimate_error' which
takes a pandas dataframe with the same column names as the provided dataset as the
argument and returns the tuple (RMSE, MAE), where RMSE is Root Mean Squared Error
and MAE is Mean Absolute Error of the model. Define the function as follows:

                               def Estimate_error(dataframe)  
                               .....  
                               return [RMSE, MAE]
