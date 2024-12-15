This repository was created during my undergraduate years to implement an automated trading system for the korean stock market. It is based on the Kiwoom Securities API and the Qt framework. It was implemented on the Windows operating system.

To implement a custom trading strategy, the user must define a class that inherits from the ***Trader*** class. The Trader class includes a virtual function called ***trade()***, which the user must override and implement. Through the member functions of Trader, users can access 30-minute and 5-minute candlestick data generated during the trading day. 

For example, to get the opening price of the 30-minute candlestick formed between 9:30 and 10:00, the user can call the function *get_chart_data_30min("A123456", 93000, OPEN)*. In addition to receiving candlestick data, users can also place orders and retrieve information about their balance and holdings through the functions provided by the Trader class.

These are the functions provided by default in the Trader class:
```
    /* Orders at limit price */
    QString buy_order_at_limit_price(QString code, int price, int quantity);
    QString sell_order_at_limit_price(QString code, int price, int quantity);

    QString modify_buy_order_at_limit_price(QString originOrderNo, int price, int quantity = 0); // quantity = 0 means all remained quantity
    QString modify_sell_order_at_limit_price(QString originOrderNo, int price, int quantity = 0);// quantity = 0 means all remained quantity

    QString cancel_buy_order_at_limit_price(QString originOrderNo, int quantity = 0); // quantity = 0 means all remained quantity
    QString cancel_sell_order_at_limit_price(QString originOrderNo, int quantity = 0); // quantity = 0 means all remained quantity

    /* Orders at conditional price */
    QString sell_order_at_conditional_price(QString code, int price, int quantity);

    /* Orders at market price */
    QString sell_order_at_market_price(QString code, int quantity);

    /* Wait */
    void wait_until(int time);

    /* Get buyable money */
    int get_money();

    /* Get sellable quantity */
    int get_sellable(QString code);

    /* Register for real data */
    /* Return screen number */
    QStringList register_code_for_real_data(QStringList codeList, FID type);

    /* Remove real data screen */
    void unregister_screen(QString screennum);

    /* 현재가 구하기 */
    int get_FID(QString code, FID fid);

    /* 보유 중인 종목 리스트 구하기 */
    QStringList get_holding_code_list();

    /* 차트 데이터 구하기 */
    int get_chart_data_30min(QString code, int time, ChartDataType type);
    int get_chart_data_5min(QString code, int time, ChartDataType type);

    /* 코스닥 혹은 코스피의 모든 종목 코드 구하기 */
    QStringList get_code_list(MarketType marketType);

    /* 대기중인 주문번호 리스트 구하기 */
    QStringList get_buy_order_number_list(QString code);
    QStringList get_sell_order_number_list(QString code);
```

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
