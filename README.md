This repository was created during my undergraduate years to implement an automated trading system for the korean stock market. It is based on the Kiwoom Securities API and the Qt framework. It was implemented on the Windows operating system.

To implement a custom trading strategy, the user must define a class that inherits from the ***Trader*** class. The Trader class includes a virtual function called ***trade()***, which the user must override and implement. Through the member functions of Trader, users can access 30-minute and 5-minute candlestick data generated during the trading day. 

For example, to get the opening price of the 30-minute candlestick formed between 9:30 and 10:00, the user can call the function *get_chart_data_30min("A123456", 93000, OPEN)*. Users can place sell orders using functions starting with *sell_order_* or place buy orders using functions starting with *buy_order_*.

In the main function, users must declare variables to manage the Trader classes and the GUI as follows:
```
ControlCenter* center = new ControlCenter;
CenterBoard w;
```
Then, they can create and register their custom traders as shown below:
```
trader_0* t = new trader_0(info);
center->employ(t, "trader0", 0);

w.board(center);
w.show();
```

After this setup, users can login to Kiwoom Securities and register an account number via the GUI, and the traders will begin trading.

The price and volume data provided by the Trader class are only for data generated during the current trading day. To access historical data from previous days, users must use their own database.
