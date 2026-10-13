void main() {
  List<String> myBooks = ['JJK', 'AOT', 'OPM', 'DBZ'];
  int itemQuantity = 2;
  double itemPrice = 1299.50;
  bool hasVoucher = true;
  
  double rawTotal = itemQuantity * itemPrice;
  double voucherDiscount = hasVoucher ? 250.0 : 0.0;
  double finalAmount = rawTotal - voucherDiscount;

  int installmentMonths = 4;
  int monthlyPayment = finalAmount ~/ installmentMonths; 
  int remainderFee = (finalAmount % installmentMonths).toInt(); 

  bool qualifiesForFreeShipping = finalAmount >= 2000.0;
  bool isHighValuePurchase = finalAmount > 5000.0;
  
  print('Enter The Book Name: ');
  
  try {
    String? rawInput = stdin.readLineSync();
    
    if (rawInput == null || rawInput.trim().isEmpty) {
      throw FormatException('Book entry cannot be blank.');
    }
    
    String userInput = rawInput.toUpperCase().trim();
    
    if (myBooks.contains(userInput)) {
      print('\nYou Borrowed the book successfully!\n');
      
      print('--- ORDER CHECKOUT RECEIPT ---');
      print('Item Purchased: $userInput'); 
      print('Quantity: $itemQuantity @ PHP $itemPrice each');
      print('Voucher Applied: $hasVoucher');
      print('--------------------------------');
      print('Subtotal: PHP $rawTotal');
      print('Final Total (After Discount): PHP $finalAmount');
      print('Monthly Installment ($installmentMonths mos): PHP $monthlyPayment (Extra cents: $remainderFee)');
      print('Qualifies for Free Shipping: $qualifiesForFreeShipping');
      print('High-Value Transaction Notice: $isHighValuePurchase');
      print('--------------------------------');
      
    } else { 
      print('Invalid Book: That title does not exist in our system.');
    }

  } on FormatException catch (e) {
    print('Input Error: ${e.message}');
  } catch (e) {
    print('An unexpected error occurred: $e');
  }
}
