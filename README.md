#include <stdio.h> #include<stdlib.h> #include<string.h>
#defineMAX_ACCOUNTS100


structAccount{
intaccountNumber;
characcountHolder[100]; float balance;
};


structBank {
structAccountaccounts[MAX_ACCOUNTS]; int count;



};


voidcreateAccount(structBank*bank){ if (bank->count == MAX_ACCOUNTS) {
printf("Cannotcreatemoreaccounts.Maximumlimitreached.\n"); return;
}


struct Account account; printf("Enteraccountnumber:");
scanf("%d",&account.accountNumber); printf("Enter account holder name: ");
getchar(); // Clear newline character from previous input fgets(account.accountHolder,sizeof(account.accountHolder),stdin); printf("Enter initial deposit amount: ");
scanf("%f",&account.balance);


bank->accounts[bank->count]=account; bank->count++;

printf("Accountcreatedsuccessfully!\n");
}


structAccount*findAccount(structBank*bank,intaccountNumber){



for(inti=0;i<bank->count;i++){
if(bank->accounts[i].accountNumber==accountNumber){ return&bank->accounts[i];
}
}
returnNULL;
}


voiddeposit(structBank*bank){ int accountNumber;
printf("Enteraccountnumber:"); scanf("%d", &accountNumber);

structAccount*account=findAccount(bank,accountNumber); if (account != NULL) {
floatamount;
printf("Enterdepositamount:"); scanf("%f", &amount);
account->balance+=amount;
printf("Successfullydeposited$%.2ftoaccount%d\n",amount,accountNumber);
}else{
printf("Accountnotfound!\n");
}
}





voidwithdraw(structBank*bank){ int accountNumber;
printf("Enteraccountnumber:"); scanf("%d", &accountNumber);

structAccount*account=findAccount(bank,accountNumber); if (account != NULL) {
floatamount;
printf("Enterwithdrawalamount:"); scanf("%f", &amount);
if(amount>account->balance){
printf("Insufficientbalanceinaccount%d\n",accountNumber);
}else{
account->balance-=amount;
printf("Successfullywithdrew$%.2ffromaccount%d\n",amount,accountNumber);
}
}else{
printf("Accountnotfound!\n");
}
}


voidbalanceEnquiry(structBank*bank){ int accountNumber;



printf("Enteraccountnumber:"); scanf("%d", &accountNumber);

structAccount*account=findAccount(bank,accountNumber); if (account != NULL) {
printf("AccountBalance:$%.2f\n",account->balance);
}else{
printf("Accountnotfound!\n");
}
}


voiddisplayDetails(structBank*bank){ int accountNumber;
printf("Enteraccountnumber:"); scanf("%d", &accountNumber);

structAccount*account=findAccount(bank,accountNumber); if (account != NULL) {
printf("AccountNumber:%d\n",account->accountNumber); printf("Account Holder: %s", account->accountHolder); printf("Balance: $%.2f\n", account->balance);
}else{
printf("Accountnotfound!\n");
}



}


voidcloseAccount(structBank*bank){ int accountNumber;
printf("Enteraccountnumber:"); scanf("%d", &accountNumber);

for(inti=0;i<bank->count;i++){
if(bank->accounts[i].accountNumber==accountNumber){ for (int j = i; j < bank->count - 1; j++) {
bank->accounts[j]=bank->accounts[j+1];
}
bank->count--;
printf("Accountclosedsuccessfully!\n"); return;
}
}
printf("Accountnotfound!\n");
}


intmain(){
structBankbank; bank.count = 0;



intchoice; do {
printf("BankingManagementSystem\n"); printf("1. Create Account\n");
printf("2. Deposit Money\n"); printf("3. Withdraw Money\n"); printf("4. Balance Enquiry\n"); printf("5.ShowAccountDetails\n"); printf("6. Close Account\n"); printf("7. Quit\n");
printf("Enteryourchoice:"); scanf("%d", &choice);

switch(choice){ case 1:
createAccount(&bank); break;
case2:
deposit(&bank); break;
case3:
withdraw(&bank); break;
case4:



balanceEnquiry(&bank); break;
case5:
displayDetails(&bank); break;
case6:
closeAccount(&bank); break;
case7:
printf("Quittingtheprogram...\n"); break;
default:
printf("Invalidchoice!Pleasetryagain.\n");
}
printf("\n");
} while(choice!=7);


return0;
}
