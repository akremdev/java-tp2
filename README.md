# java-tp2

```java
package jdbcdema;
import java.sql.*;
public class Driver {
public static void main(String[] args) throws SQLException {
Connection myConn = null;
Statement myStmt = null;
Statement myStmt2 = null;
Statement myStmt3 = null;
ResultSet rs = null;
ResultSet myRs = null;
ResultSet myRs2 = null;
PreparedStatement rechUser = null;
try {
// 1. Get a connection to database
myConn =
DriverManager.getConnection("jdbc:mysql://localhost/test",
"root" , "toorroot");
// 2. Create a statement
myStmt = myConn.createStatement(
ResultSet.TYPE_SCROLL_SENSITIVE,
ResultSet.CONCUR_UPDATABLE);
String sql = "SELECT * FROM employees";
ResultSet resultat= myStmt.executeQuery(sql);
resultat.first();
String n1 = resultat.getString("first_name");
resultat.updateString("first_name","akrem");
resultat.updateRow();String n2 = resultat.getString("first_name");
System.out.println(n1+" "+n2);
myConn.setAutoCommit(false);
myStmt2 = myConn.createStatement();
myStmt2.addBatch("INSERT INTO employees VALUES ('EL HAK
','SALMA,'salma@gmail.com' )");
myStmt2.addBatch("INSERT INTO employees VALUES ('Ali ','ben
ali','ali@yahoo.fr' )");
myStmt2.addBatch("INSERT INTO employees VALUES
('mohamed','ben mohamed,'mohamed12@hotmail.com' )");
myStmt2.addBatch("INSERT INTO employees VALUES ('fathi','ben
fathi,'fathi20@outlook.com' )"); myStmt2.executeBatch();
System.out.println("succée");
myStmt3 = myConn.createStatement();
// 3. Execute SQL query
myRs2 = myStmt3.executeQuery("select * from employees");
// 4. Process the result set
while (myRs2.next()) {
System.out.println(myRs2.getString("last_name") + ", " +
myRs2.getString("first_name"));
}
myConn.commit();
rechUser = myConn.prepareStatement("SELECT * FROM
employees WHERE adress = ?");
rechUser.setString(1, "Tunis");
rs = rechUser.executeQuery();
System.out.println("parcours des données retournées");
while(rs.next()) {
System.out.print("(" + rs.getString(1) + " : "+rs.getString(2) + " :
"+rs.getString(3) + " : "+rs.getString(4)+ " : "+rs.getString(5)+")");
System.out.println();
}
rs.close();} catch (Exception exc) {
exc.printStackTrace();
} finally {
if (myRs != null)
{
myRs.close();
}
if (myStmt != null)
{
myStmt.close();
}
if (myConn != null)
{
myConn.close()
;
}
}
}
}
```
