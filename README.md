# Data-Sources-for-IBKR-Trading-Bot
from ibapi.client import EClient
from ibapi.wrapper import EWrapper
from ibapi.contract import Contract

class IBApp(EWrapper, EClient):
    def __init__(self):
        EClient.__init__(self, self)
        self.data = []

    def historicalData(self, reqId, bar):
        self.data.append([bar.date, bar.close])

app = IBApp()
app.connect("127.0.0.1", 7497, clientId=1)
contract = Contract()
contract.symbol = "AAPL"
contract.secType = "STK"
contract.exchange = "SMART"
contract.currency = "USD"
app.reqHistoricalData(1, contract, "", "1 D", "1 min", "TRADES", 0, 2, False, [])
