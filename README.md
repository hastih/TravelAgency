package TravelAgency;

import javafx.application.Application; 
import static javafx.application.Application.launch;

import java.net.URL;

import javafx.scene.paint.Color;
import javafx.geometry.Insets; 
import javafx.geometry.Pos;
import javafx.geometry.Rectangle2D;
import javafx.scene.Cursor;
import javafx.scene.Group;
import javafx.scene.Scene; 
import javafx.scene.control.Button; 
import javafx.scene.control.PasswordField;
import javafx.scene.layout.BorderPane;
import javafx.scene.layout.GridPane;
import javafx.scene.layout.HBox;
import javafx.scene.layout.StackPaneBuilder;
import javafx.scene.layout.VBox;
import javafx.scene.text.Text; 
import javafx.scene.control.TextField;
import javafx.scene.control.ToggleButton;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.stage.Stage;  
import javafx.scene.input.MouseEvent;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;

/**
 *  This class shows a 
 */
         
public class HomePageRegisteredUsers extends Application { 
    /**
     *  start method
     * 
     *  The fields and buttons are added to a GridPane, which is added
     *  to the Scene.
     *  @param stage The window to be displayed.
     */
    @Override 
    public void start(Stage stage) {      
        
        
        Button LogOut =new Button("Log out");
        LogOut.setCursor(Cursor.HAND);
        LogOut.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
            	HomePage homepage = null;
				try {
					homepage = new HomePage();
				} catch (Exception e1) {
					// TODO Auto-generated catch block
					e1.printStackTrace();
				}
            	try {
					homepage.start(stage);
				} catch (Exception e) {
					e.printStackTrace();
				}
            	stage.show();
                
            }

        });
        
        Button booking =new Button("Booking");
        booking.setCursor(Cursor.HAND);
        booking.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
            	Booking BookingPage = new Booking();
            	try {
            		BookingPage.start(stage);
				} catch (Exception e) {
					e.printStackTrace();
				}
            	stage.show();
                
            }

        });
        
        Button AboutUsB =new Button("About Us");
        AboutUsB.setCursor(Cursor.HAND);
        AboutUsB.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
            	AboutUs AboutUspage2 = new AboutUs();
            	try {
            		AboutUspage2.start(stage);
				} catch (Exception e) {
					e.printStackTrace();
				}
            	stage.show();
                
            }

        });
        
        Button OrderMealButton =new Button("Order Your Special Meal");
        OrderMealButton.setCursor(Cursor.HAND);
        OrderMealButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
            	OrderMeal OrderMealpage = new OrderMeal();
            	try {
            		OrderMealpage.start(stage);
				} catch (Exception e) {
					e.printStackTrace();
				}
            	stage.show();
                
            }

        });
        
        Button TicketStatusButton =new Button("Ticket Status");
        TicketStatusButton.setCursor(Cursor.HAND);
        TicketStatusButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
            	TicketStatus TicketStatuspage = new TicketStatus();
            	try {
            		TicketStatuspage.start(stage);
				} catch (Exception e) {
					e.printStackTrace();
				}
            	stage.show();
                
            }

        });
        
        VBox vbox = new VBox(8);  // spacing = 8
        vbox.getChildren().addAll(new Button("Latest news"),AboutUsB,new Button("Contact"));
        
        HBox hbox = new HBox(4);  // spacing = 4
        hbox.getChildren().addAll(booking,TicketStatusButton, OrderMealButton,LogOut);
        
        URL img = getClass().getResource("travel.jpg");
		String imgUrl = img.toExternalForm();
        Image image = new Image(imgUrl);
        
        // defines a viewport into the source image (achieving a "zoom" effect) and
        // displays it rotated
        ImageView iv3 = new ImageView();
        iv3.setImage(image);
        //Rectangle2D viewportRect = new Rectangle2D(40, 35, 110, 110);
        //iv3.setViewport(viewportRect);
        //iv3.setRotate(90);
        iv3.setFitWidth(900);
        iv3.setFitHeight(500);
        //iv3.setPreserveRatio(true);
        iv3.setSmooth(true);
        iv3.setCache(true);


        
        //Creating a Grid Pane 
        GridPane gridPane = new GridPane();    
      
        //Setting the vertical and horizontal gaps between the columns 
        gridPane.setVgap(5); 
        gridPane.setHgap(5);       
        gridPane.setPadding(new Insets(10, 10, 10, 10));       
      
        //Adding the nodes to the grid 
        gridPane.add(iv3, 1, 10);
        gridPane.add(vbox, 0, 10);
        gridPane.add(hbox, 1, 8);
        
        gridPane.setStyle("-fx-background-color: #DCDCDC;"+
        		"-fx-padding: 10;" +
				"-fx-border-style: solid inside;" +
				"-fx-border-width: 2;" +
				"-fx-border-insets: 5;" +
				"-fx-border-radius: 5;" +
				"-fx-border-color: #4B0082;");
        
        Group root = new Group(gridPane);
        //Creating a scene object 
        Scene scene = new Scene(root, 1200, 600, Color.GAINSBORO); 
       
        //Setting title to the Stage 
        stage.setTitle("Home page"); 
        
        //Adding scene to the stage 
        stage.setScene(scene);
        //Displaying the contents of the stage 
        stage.show(); 
    }      

    /*
     *  main method to launch the application.
     */
    public static void main(String args[]){ 
    	
        launch(args); 
    } 
}
