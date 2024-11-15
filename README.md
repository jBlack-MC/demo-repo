#demo

some coding!!
package prog1ex;

/**
 *
 * @author RC_Student_lab
 */
public class Prog1ex {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        // Array to hold the movies
        String[] movies = {"Napoleon", "Oppenheimer"};
        // 2D array for the sales values
        int[][] sales = {{3000, 1500, 1700}, {3500, 1200, 1600}};
        
        // Print header for the sales table
        System.out.println("MOVIE TICKET SALES REPORT - 2024 \n");
        System.out.println("\t\t JAN \t\t FEB\t\t MAR ");
        System.out.println("**********************************************************");
        
        int[] total = new int[movies.length];
        IMovieTickets salesCalculator = new MovieTickets();

        // Loop through each MOVIE
        for (int i = 0; i < sales.length; i++) {
            // Print the MOVIE
            System.out.print(movies[i] + "\t");
            // Print the sales for each month
            for (int j = 0; j < sales[i].length; j++) {
                System.out.print(sales[i][j] + "\t\t"); // Print sales for the month
            }
            // Calculate the total sales for the current movie
            total[i] = salesCalculator.calculateTotalSales(sales, i);
            // Print the total sales for the current movie
            System.out.print(total[i] + " \t");
            // Move to the next line 
            System.out.println();
        }
      
        // Display the movie with the highest total sales
        String highestSalesMovie = salesCalculator.findMovieWithHighestSales(movies, total);
        System.out.println("Movie with the highest total sales: " + highestSalesMovie);
    }
}


package prog1ex;

/**
 *
 * @author RC_Student_lab
 */
public interface IMovieTickets {
    int calculateTotalSales(int[][] sales, int movieIndex);

    String findMovieWithHighestSales(String[] movies, int[] totalSales);
}
.               


package prog1ex;

/**
 *
 * @author RC_Student_lab
 */
public class MovieTickets implements IMovieTickets {
    @Override
    public int calculateTotalSales(int[][] sales, int movieIndex) {
        int total = 0;
        for (int k = 0; k < sales[movieIndex].length; k++) {
            total += sales[movieIndex][k];
        }
        return total;
    }

    @Override
    public String findMovieWithHighestSales(String[] movies, int[] totalSales) {
        int maxTotal = 0;
        int maxIndex = -1;

        for (int i = 0; i < totalSales.length; i++) {
            if (totalSales[i] > maxTotal) {
                maxTotal = totalSales[i];
                maxIndex = i;
            }
        }

        return maxIndex != -1 ? movies[maxIndex] + " with total sales of " + maxTotal : "No sales data available.";
    }
}


import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.AfterAll;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

/**
 *
 * @author RC_Student_lab
 */
public class NewEmptyJUnitTest {
    
    public NewEmptyJUnitTest() {
    }
    
    @BeforeAll
    public static void setUpClass() {
    }
    
    @AfterAll
    public static void tearDownClass() {
    }
    
    @BeforeEach
    public void setUp() {
    }
    
    @AfterEach
    public void tearDown() {
    }

    // TODO add test methods here.
    // The methods must be annotated with annotation @Test. For example:
    //
    // @Test
    // public void hello() {}
    @Test
    public void testFindMovieWithHighestSales() {
        String[] movies = {"Napoleon", "Oppenheimer"};
        int[][] sales = {{3000, 1500, 1700}, {3500, 1200, 1600}};
        int[] totalSales = {6200, 6300};
        
        MovieTickets salesCalculator = new MovieTickets();
        
        // Test finding the movie with the highest total sales
        assertEquals("Oppenheimer with total sales of 6300", salesCalculator.findMovieWithHighestSales(movies, totalSales));
        
        // Test with a different scenario
        int[] totalSales2 = {0, 0}; // All zero sales
        assertEquals("No sales data available.", salesCalculator.findMovieWithHighestSales(movies, totalSales2));
    }
}
