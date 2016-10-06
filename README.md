# code


import java.sql.*;
import  java.io.*;  
import java.sql.CallableStatement;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.Scanner;

public class a12 {
                               

  static final String url = "jdbc:mysql://localhost:3306/test";
	    static final String username="root";
	    static final String password="";
    public static void main(String a[])
	 {
                      
                   
	   Connection con=null;
                   
         boolean flag=true; 
                int ch,y;
                 try
	       {
		System.out.println("Connecting Database..");
		con=DriverManager.getConnection(url,username,password);
		System.out.println("Database Connected..");
                               CallableStatement cs = null;
		Statement stmnt=con.createStatement();
                          do
                 {
                        Scanner in = new Scanner(System.in);
                        System.out.println("1.Create table");
                        System.out.println("2.Insert table");
			System.out.println("3.Display table");
			System.out.println("4.Update table");
			System.out.println("5.Delete table");                
        		System.out.println("Enter your choice:");
	
                     
	        ch=in.nextInt();
              switch(ch)
	{
	   case 1:    
                 System.out.println("Creating Table....");
		 String p="create table employe( id int(10),"+"fname varchar(15),"+"lname varchar(15),"+"ag int(10))";
		 stmnt.executeUpdate(p);
		 System.out.println("Table..created..");
                              break;

                 case 2:
                                           
			System.out.println("Enter  id : ");
			int id = in.nextInt();
                        String str = in.nextLine();

                System.out.println("Enter Employee fname:");
                        String f = in.nextLine();  
   
			System.out.println("Enter last name: ");
                        String l = in.nextLine();
			
                        System.out.println("Enter age:");
                        int ag = in.nextInt();
						
			PreparedStatement pStmt = con.prepareStatement("insert into employe values(?,?,?,?)");
			pStmt.setInt(1,id);
			pStmt.setString(2,f);
			pStmt.setString(3,l);
			pStmt.setInt(4,ag);
			pStmt.executeUpdate();
                                   break;

                     case 3:    String s="select  *  from employe";
	                     ResultSet rs1 = stmnt.executeQuery(s);
                                    System.out.println("ID"+"\tFNAME"+"\tLNAME"+"\t AGE  ");
                                     while(rs1.next()){
                             System.out.println(rs1.getInt(1)+"\t" +rs1.getString(2)+"\t " +rs1.getString(3)+"\t " +rs1.getInt(4));
                                      }
                                      break;

                     case 4:
			String sq  = "UPDATE employe SET id=?, fname=?, lname=? WHERE ag=?";

			System.out.println("Enter the age of employee whose data needs to be updated:");
                        int ag1 = in.nextInt();

			System.out.println("Enter  id : ");
			int id1 = in.nextInt();
                        String str1 = in.nextLine();

                        System.out.println("Enter Employee fname:");
                        String f1 = in.nextLine();  
   
			System.out.println("Enter last name: ");
                        String l1 = in.nextLine();
			
                        			PreparedStatement pStmt1 = con.prepareStatement(sq);
		pStmt1.setInt(1,id1);
		pStmt1.setString(2,f1);
		pStmt1.setString(3,l1);
		pStmt1.setInt(4,ag1);
		pStmt1.executeUpdate();
		break;                            

		case 5:
String sql = "DELETE FROM employe WHERE id=?";
System.out.println("Enter  id : ");
			int id2 = in.nextInt(); 
PreparedStatement statement = con.prepareStatement(sql);
statement.setInt(1,id2 );

statement.executeUpdate();
break;


               }
        
                 System.out.println("do u want to continue(1 /0)");  
                  y=in.nextInt();
                       } while(y==1);  
    
   }

                catch(SQLException e)
		{
			System.err.println("Cannot connect the database!..");
			e.printStackTrace();
		}
		finally
		{
			System.out.println("Closing the connection..");
			if(con!=null) try{ con.close(); } catch(SQLException ignore){}
		}


}

}
