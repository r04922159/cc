type Account struct{
	string ID
	dictionary Ostock
	string Password
}
type Stock struct{
	string Company
	float Price
	boolean maxrise
	boolean maxfall
}

func Getstock(string company, chaincodestub){
	comp = chaincodestub.Getstate(company)
	comp = json.Unmarshal(comp)
	return comp
}

func Query(chaincodestub, function string, args string) {
	if args[0] == "Getstock" {
		tstock = Getstock(args[1], chaincodestub)
		tstock = json.Marshal(&tstock)	
		return tstock
	}
	return error
}

func createAccount(chaincodestub, string args[]){
	Account account
	if len(args) != 1{
		return nil
	}
	from chaincodestub verify the certification
		and if there is any existing account with the same ID
	username = args[0]
	ostock = {}
	password = random string of length 10
	account = {ID: username, Ostock: ostock, Password: password}
	chaincodestub.PutState(account)
}

func transfer(chaincodestub, string args[]){
	Account account
	Stock stock
	if len(args) != 1{
		return nil
	}
	from chaincode verify the certification
	json.Unmarshal(args[0], &tx)	
	stock = from tx import the stock state we need(company, stock price, rise/fall of the stock)
	account = from tx import the account state
	if (stock.maxrise == true && tx.action == "buy") || (stock.maxfall == true && tx.action == "sell"){
		return nil
	}
	if tx.action == "buy"{
		if tx.stock in account.Ostock{
			account.Ostock["tx.stock"] += tx.amount
		}
	}
	else{
		if (tx.stock not in account.Ostock) || (tx.amount > account.Ostock["tx.stock"]){
			return nil
		} 
		account.Ostock["tx.stock"] -= tx.amount
	}
	chaincodestub.Putstate(account)	
}

func Run(chaincodeStub, function string, string args[]){
	if function == "createAccount"{
		return createAccount(chaincodestub, args)
	}
	else if function == "transfer"{
		return transfer(chaincodestub, args)
	}

	return fail message
}


























func main(){


}