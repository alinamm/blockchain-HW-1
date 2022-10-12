# blockchain-HW-1

## Task 1
```
@@ -291,6 +291,8 @@ contract MultiSigWallet {
         notNull(destination)
         returns (uint transactionId)
     {
+        require(value <= 66 ether, "Not more than 66 ether at one transaction");
+
         transactionId = transactionCount;
         transactions[transactionId] = Transaction({
             destination: destination,
```

## Task 2
```
@@ -230,6 +230,7 @@ contract ERC20 is Context, IERC20, IERC20Metadata {
     ) internal virtual {
         require(from != address(0), "ERC20: transfer from the zero address");
         require(to != address(0), "ERC20: transfer to the zero address");
+        require((block.timestamp / 1 days + 3) % 7 != 5, "ERC20: can not transfer on Saturday");

         _beforeTokenTransfer(from, to, amount);
```
     
## Task 3
```
@@ -18,7 +18,7 @@ contract DividendToken is StandardToken, Ownable {
     event PayDividend(address indexed to, uint256 amount);
     event HangingDividend(address indexed to, uint256 amount) ;
     event PayHangingDividend(uint256 amount) ;
-    event Deposit(address indexed sender, uint256 value);
+    event Deposit(address indexed sender, uint256 value, bytes[32] comment);

     /// @dev parameters of an extra token emission
     struct EmissionInfo {
@@ -37,9 +37,9 @@ contract DividendToken is StandardToken, Ownable {
         }));
     }

-    function() external payable {
+    function(bytes[32] comment) external payable {
         if (msg.value > 0) {
-            emit Deposit(msg.sender, msg.value);
+            emit Deposit(msg.sender, msg.value, comment);
             m_totalDividends = m_totalDividends.add(msg.value);
         }
     }
```
