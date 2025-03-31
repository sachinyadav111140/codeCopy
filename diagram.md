
graph TD;
    Farmer-->MilkCollection;
    Buyer-->MilkCollection;
    MilkCollection-->Invoice;
    MilkCollection-->Payment;
    Invoice-->NotificationService;
    Payment-->BankIntegration;
    WebApp-->APIService;
    APIService-->MilkCollection;
    APIService-->Invoice;
    APIService-->Payment;
