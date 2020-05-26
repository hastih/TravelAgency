package TravelAgency;

import java.io.IOException;
import java.util.ArrayList;

import javax.naming.ConfigurationException;

import javafx.application.Application;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.geometry.Pos;
import javafx.scene.Cursor;
import javafx.scene.Scene;
import javafx.scene.control.Alert;
import javafx.scene.control.Button;
import javafx.scene.control.TextField;
import javafx.scene.layout.GridPane;
import javafx.scene.layout.StackPane;
import javafx.scene.paint.Color;
import javafx.scene.control.Alert.AlertType;
import javafx.scene.text.Font;
import javafx.scene.text.Text;
import javafx.stage.Stage;

public class TicketStatus extends Application{
	Traveler customer = null;
	@Override
	public void start(Stage stage) throws Exception {
		GridPane Gpane = new GridPane();
		Font myFont = new Font("Segoe Print", 15);
		Font myFont2 = new Font("Segoe Print", 15);
		Text ticketNOText = new Text("Please enter your ticket number:");
		ticketNOText.setFont(myFont);
		TextField ticketNOTextField = new TextField();
		
		Button OKButton =new Button("OK");
		OKButton.setCursor(Cursor.HAND);
		OKButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
            	if(ticketNOTextField.getText().equals("")) {
            		Alert Empty = new Alert(AlertType.ERROR);
            		Empty.setTitle("Warning!");
            		Empty.setContentText("Please enter your ticket number");
            		Empty.show();
            	}
            	
            	else {
            		try {
            			String [] Tinputs= {"TravelList",ticketNOTextField.getText()};
            			HomePage.dos.writeObject(Tinputs);
            			customer = (Traveler) HomePage.dis.readObject();
            		} catch (IOException e) {
            			e.printStackTrace();
            		} catch (ClassNotFoundException e) {
            			e.printStackTrace();
            		}
                	
                	if(customer==null) {
            			Alert WarningAlert = new Alert(AlertType.ERROR);
                		WarningAlert.setTitle("Warning!");
                		WarningAlert.setContentText("You've not booked any ticket with this ticket number");
            			WarningAlert.show();
            		}
                	else {
                		 Text ConfText = new Text("Your ticket is booked sucessfully");
                		 ConfText.setFont(myFont2);
                		 Text TfirstnameText = new Text(customer.TravelerFirstName);
                		 TfirstnameText.setFont(myFont2);
                		 Text TlastnameText = new Text(customer.TravelerLastname);
                		 TlastnameText.setFont(myFont2);
                		 Text TDOBText = new Text(customer.TravelerDateOfBirth);
                		 TDOBText.setFont(myFont2);
                		 Text TpassNOText = new Text(customer.TravelerPassportNumber);
                		 TpassNOText.setFont(myFont2);
                		 Text TnationalityText = new Text(customer.TravelerNationality);
                		 TnationalityText.setFont(myFont2);
                		 Text TticketNOText = new Text(customer.TravelerTicketNumber);
                		 TticketNOText.setFont(myFont2);
                		 Text TdepartureText = new Text(customer.TravelerDeparture);
                		 TdepartureText.setFont(myFont2);
                		 Text TdestinationText = new Text(customer.TravelerDestination);
                		 TdestinationText.setFont(myFont2);
                		 Text TfromdateText = new Text(customer.TravelFromDate);
                		 TfromdateText.setFont(myFont2);
                		 Text TtodateText = new Text(customer.TravelToDate);
                		 TtodateText.setFont(myFont2);
                		 Text airline1Text = new Text(customer.AirlineName1);
                		 airline1Text.setFont(myFont2);
                		 Text time1Text = new Text(customer.TravelTime1);
                		 time1Text.setFont(myFont2);
                		 Text airline2Text = new Text(customer.AirlineName2);
                		 airline2Text.setFont(myFont2);
                		 Text  time2Text = new Text(customer.TravelTime2);
                		 time2Text.setFont(myFont2);
                		 Text TmealText = new Text(customer.TravelerMeal);
                		 TmealText.setFont(myFont2);
                		 Gpane.add(ConfText, 0, 1);
                		 Gpane.add(TfirstnameText, 1, 2);
                		Gpane.add(TlastnameText, 2, 2);
                		Gpane.add(TDOBText, 1, 3);
                		Gpane.add(TpassNOText, 1, 4);
                		Gpane.add(TnationalityText, 1, 5);
                		Gpane.add(TticketNOText, 1, 6);
                		Gpane.add(TdepartureText, 1, 7);
                		Gpane.add(TdestinationText, 3, 7);
                		Gpane.add(TfromdateText, 1, 8);
                		Gpane.add(TtodateText, 3, 8);
                		Gpane.add(airline1Text, 0, 9);
                		Gpane.add(time1Text, 1, 9);
                		Gpane.add(airline2Text, 0, 10);
                		Gpane.add(time2Text, 1, 10);
                		Gpane.add(TmealText, 0, 11);
                	}
            	}
            }

        });
		Text text1 = new Text("Your Name: ");
		text1.setFont(myFont2);
		Text text2 = new Text("Your Date of Birth: ");
		text2.setFont(myFont2);
		Text text3 = new Text("Passport Number: ");
		text3.setFont(myFont2);
		Text text4 = new Text("Nationality: ");
		text4.setFont(myFont2);
		Text text5 = new Text("Your Ticket Number: ");
		text5.setFont(myFont2);
		Text text6 = new Text("Departure: ");
		text6.setFont(myFont2);
		Text text7 = new Text("Destination: ");
		text7.setFont(myFont2);
		Text text8 = new Text("From: ");
		text8.setFont(myFont2);
		Text text9 = new Text("To: ");
		text9.setFont(myFont2);
		
		Button HomePageB =new Button("Back to Home Page");
        HomePageB.setCursor(Cursor.HAND);
        HomePageB.setStyle("-fx-background-color: #B0C4DE");
        HomePageB.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
            	HomePageRegisteredUsers BackToHomePage2 = new HomePageRegisteredUsers();
	            	try {
	            		BackToHomePage2.start(stage);
					} catch (Exception e) {
						e.printStackTrace();
					}
	            	stage.show();
                
            }

        });
		
		Gpane.add(ticketNOText, 0, 0);
		Gpane.add(ticketNOTextField, 1, 0);
		Gpane.add(OKButton, 2, 0);
		
		Gpane.add(text1, 0, 2);
		
		Gpane.add(text2, 0, 3);
		
		Gpane.add(text3, 0, 4);
		
		Gpane.add(text4, 0, 5);
		
		Gpane.add(text5, 0, 6);
		
		Gpane.add(text6, 0, 7);
		
		Gpane.add(text7, 2, 7);
		
		Gpane.add(text8, 0, 8);
		
		Gpane.add(text9, 2, 8);
		Gpane.add(HomePageB, 0, 12);
		Gpane.setAlignment(Pos.CENTER);
		
		StackPane mainroot = new StackPane();
       	mainroot.setId("pane");
       	mainroot.getChildren().add(Gpane);
       	mainroot.setStyle("-fx-padding: 10;" +
				"-fx-border-style: solid inside;" +
			"-fx-border-width: 2;" +
			"-fx-border-insets: 5;" +
			"-fx-border-radius: 5;" +
			"-fx-border-color: #4B0082;"+
			"-fx-background-color: #DCDCDC;");
		
		
		
        Scene scene = new Scene(mainroot, 1200, 600, Color.GAINSBORO); 
        scene.getStylesheets().addAll(this.getClass().getResource("style.css").toExternalForm());
        //Setting title to the Stage 
        stage.setTitle("Ticket Status"); 
        //Adding scene to the stage 
        stage.setScene(scene);
        //Displaying the contents of the stage 
        stage.show();
	}

}
