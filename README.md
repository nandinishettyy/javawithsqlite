# javawithsqlite
package databasepackage;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.ArrayList;

public class Main {

	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		createTable();
		post();
		get();
	}
	public static ArrayList<String> get() throws Exception{
		try {
			Connection conn = getConnection();
			PreparedStatement statement = conn.prepareStatement("SELECT * FROM movies");
			ResultSet result = statement.executeQuery();
			ArrayList<String> array = new ArrayList<String>();
			while(result.next()) {
				System.out.println(result.getString("moviename"));
				System.out.println(result.getString("leadactor"));
				System.out.println(result.getString("leadactress"));
				System.out.println(result.getInt("yearofrelease"));
				System.out.println(result.getString("director"));
				array.add(result.getString("director"));
			}
			System.out.println("All record have been selected");
			return array;
		}
		catch(Exception e)
		{
			System.out.println(e);
		}
		return null;
	}

	public static void createTable() throws Exception{
		try {
			Connection conn = getConnection();
			PreparedStatement create = conn.prepareStatement( "CREATE TABLE IF NOT EXISTS movies(moviename varchar(30), yearofrelease int, leadactor varchar(30), leadactress varchar(30), director varchar(30), primary key(moviename));");
			create.executeUpdate();
		}
		catch(Exception e)
		{
			System.out.println(e);
		}
		finally{
			System.out.println("Function complete.");
			}
	}
	public static void post() throws Exception{
		final String var1 = "Padmaavat";
		final String var2 = "Ranveer Singh";
		final String var3 = "Deepika Padukone";
		final int var4 = 2018;
		final String var5 = "S L Bhansali";
		try {
			Connection conn = getConnection();
			PreparedStatement posted = conn.prepareStatement("INSERT INTO movies (moviename, leadactor, leadactress, yearofrelease, director) VALUES ('"+var1+"','"+var2+"','"+var3+"','"+var4+"','"+var5+"')");
			posted.executeUpdate();
		}
		catch(Exception e)
		{
			System.out.println(e);
		}
		finally {
			System.out.println("Insert completed");
		}
	}
	public static Connection getConnection() throws Exception{
		try {
			String driver = "org.sqlite.JDBC";
			String url = "jdbc:sqlite:/C:\\Users\\ADMIN\\Documents\\SQLite\\sqlite-tools-win32-x86-3380200\\usersdb.db";
			String username = "ADMIN";
			String password = "shetty2001";
			Class.forName(driver);
			
			Connection conn = DriverManager.getConnection(url,username,password);
			System.out.println("Connected");
			return conn;
		}
		catch(Exception e)
		{
			System.out.println(e);
		}		
		return null;
	}
}
