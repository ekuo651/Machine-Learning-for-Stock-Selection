
## Imports

```
import numpy as np
import pandas as pd
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import LSTM, Dense, Dropout
import hvplot.pandas
%matplotlib inline
```
## Functions

**Run 3 - layer LSTM**
```
def run_3_LSTM(number_units, dropout, X_train, y_train, optimizer, loss, epoch, X_test, y_test):
    rnn.add(LSTM(units=number_units, return_sequences=True, input_shape=(X_array.shape[1],1)))
    rnn.add(Dropout(drop_out))
    rnn.add(LSTM(units=number_units, return_sequences=True))
    rnn.add(Dropout(drop_out))
    rnn.add(LSTM(units=number_units, return_sequences=True))
    rnn.add(Dropout(drop_out))
    rnn.add(Dense(1))
    rnn.compile(optimizer=optimizer, loss=loss)
    rnn.fit(X_train, y_train, epochs=epoch, shuffle=False, batch_size=1, verbose=0)
    loss = rnn.evaluate(x=X_test,y=y_test)
    return loss
```

**Function that outputs parameters for various LSTM**

```
def set_parameters(input_array):
    return number_units, dropout, X_train, y_train, optimizer, loss, epoch, X_test, y_test
    
```





## Tests

```
test_1 = run_3_LSTM(20, .8, X_train_reshaped, y_train, 'adam', 'mean_squared_error', 10,X_test_reshaped, y_test)
test_2 = run_3_LSTM(20, .8, X_train_reshaped, y_train, 'sgd', 'mean_squared_error', 30,X_test_reshaped, y_test)
test_3 = run_3_LSTM(20, .8, X_train_reshaped, y_train, 'adam', 'mean_absolute_error', 10,X_test_reshaped, y_test)
test_4 = run_3_LSTM(20, .8, X_train_reshaped, y_train, 'nadam', 'mean_squared_error', 30,X_test_reshaped, y_test)
test_5 = run_3_LSTM(20, .8, X_train_reshaped, y_train, 'adam', 'mean_absolute_percentage_error', 30,X_test_reshaped, y_test)
test_6 = run_3_LSTM(20, .8, X_train_reshaped, y_train, 'adam', 'mean_squared_logarithmic_error', 30,X_test_reshaped, y_test)
test_7 = run_3_LSTM(20, .8, X_train_reshaped, y_train, 'adam', 'hinge', 40,X_test_reshaped, y_test)
test_8 = run_3_LSTM(20, .8, X_train_reshaped, y_train, 'adadelta', 'mean_squared_error', 40,X_test_reshaped, y_test)
test_9 = run_3_LSTM(20, .8, X_train_reshaped, y_train, 'adagrad', 'mean_squared_error', 40,X_test_reshaped, y_test)
test_10 = run_3_LSTM(20, .8, X_train_reshaped, y_train, 'adamax', 'mean_squared_error', 40,X_test_reshaped, y_test)
```