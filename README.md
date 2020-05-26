package TravelAgency;

import java.io.IOException;
import java.net.URL;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

import javafx.application.Application;
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.geometry.Insets;
import javafx.geometry.Pos;
import javafx.scene.Cursor;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.scene.control.Alert;
import javafx.scene.control.Button;
import javafx.scene.control.ChoiceBox;
import javafx.scene.control.DatePicker;
import javafx.scene.control.RadioButton;
import javafx.scene.control.TableColumn;
import javafx.scene.control.TableView;
import javafx.scene.control.ToggleGroup;
import javafx.scene.control.Alert.AlertType;
import javafx.scene.control.cell.PropertyValueFactory;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.scene.layout.GridPane;
import javafx.scene.layout.HBox;
import javafx.scene.paint.Color;
import javafx.scene.text.Font;
import javafx.scene.text.Text;
import javafx.stage.Stage;

public class Timetable extends Application{
	Stage window;
	Scene TimetablePage;
	private ArrayList<Airplane> dataSet = new ArrayList<>();
	@Override
	public void start(Stage Stage) throws Exception {
		window = Stage;
		Font myFont = new Font("Segoe Print", 20);
		Text fromText = new Text("From");
		fromText.setStyle("-fx-background-color: #708090");
		fromText.setFont(myFont);
		Text ToText = new Text("To");
		Text To2 = new Text("To");
		ToText.setStyle("-fx-background-color: #708090");
		ToText.setFont(myFont);
		
		DatePicker FromDateCalendar = new DatePicker();
		DatePicker ToDateCalendar = new DatePicker();
		
		ToggleGroup Tgroup = new ToggleGroup();
        RadioButton oneWay  = new RadioButton("One Way");
        oneWay.setToggleGroup(Tgroup);
        RadioButton RoundTrip  = new RadioButton("Round Trip");
        RoundTrip.setToggleGroup(Tgroup);
        oneWay.setOnAction(new EventHandler<ActionEvent>() {
			@Override
			public void handle(ActionEvent event) {
				ToDateCalendar.setVisible(false);
			}
        });
        RoundTrip.setOnAction(new EventHandler<ActionEvent>() {
			@Override
			public void handle(ActionEvent event) {
				ToDateCalendar.setVisible(true);
			}
        });
        
        ArrayList<String> cities =new ArrayList<>();
        cities.add("London");
        cities.add("Munich");
        cities.add("Stockholm");
        cities.add("Berlin");
        cities.add("Amsterdam");
        cities.add("Paris");
        cities.add("Birmingham");
        cities.add("New York");
        cities.add("Sydney");
        cities.add("Rome");
        cities.add("Milan");
        cities.add("Washington");
        cities.add("Madrid");
        cities.add("Athens");
        cities.add("Nicosia");
        cities.add("Kiev");
        cities.add("Prague");
        cities.add("Vienna");
        cities.add("Sofia");
        cities.add("Bucharest");
        cities.add("Copenhagen");
        Collections.sort(cities,new Comparator<String>(){
			@Override
			public int compare(String s1, String s2) {
				return s1.compareTo(s2);
			}
		});
        // create a choiceBox 
        ChoiceBox<String> FromList = new ChoiceBox<>(FXCollections.observableArrayList(cities));
        ChoiceBox<String> ToList = new ChoiceBox<>(FXCollections.observableArrayList(cities));
		
        ;
        
        Button search = new Button("Search Flights");
        search.setCursor(Cursor.HAND);
        search.setStyle("-fx-background-color: #B0C4DE");
        search.setOnAction(new EventHandler<ActionEvent>() {
			@SuppressWarnings({ "unchecked" })
			@Override
			public void handle(ActionEvent event) {
            	String departure="";
            	if(FromList.getValue()!=null) {
            		departure=FromList.getValue().toString();
            	}
            	String destination="";
            	if(ToList.getValue()!=null) {
            		destination=ToList.getValue().toString();
            	}
            	String Fromdate="";
            	if(FromDateCalendar.getValue()!=null) {
            		Fromdate=FromDateCalendar.getValue().toString();
            	}
            	String Todate="";
            	if(ToDateCalendar.getValue()!=null) {
            		Todate=ToDateCalendar.getValue().toString();
            	}
            	String travelType;
            	RadioButton selectedRadioButton = (RadioButton)Tgroup.getSelectedToggle();
            	if(selectedRadioButton==null) {
            		travelType="";
            	}
            	else {
            		travelType =selectedRadioButton.getText();
            	}
            	
            	if(departure.equals("") || destination.equals("") || (Fromdate.equals("") & Todate.equals(""))||
            			travelType.equals("")) {
            		Alert EmptyFieldAlert = new Alert(AlertType.INFORMATION);
            		EmptyFieldAlert.setTitle("Warning");
            		EmptyFieldAlert.setContentText("Please fill out all the blanks");
            		EmptyFieldAlert.show();
            	}
            	else {
            		if(Fromdate.compareTo(Todate)==1) {
                		Alert UnvalidDateAlert = new Alert(AlertType.INFORMATION);
                		UnvalidDateAlert.setTitle("Warning");
                		UnvalidDateAlert.setContentText("Please choose a valid date");
                		UnvalidDateAlert.show();
            		}
            		
            		
            		else {
            			String [] info= {"checkFlights",travelType,departure,destination, Fromdate,Todate};
            			
            				try {
            					HomePage.dos.writeObject(info);
            					dataSet.addAll((ArrayList<Airplane>) HomePage.dis.readObject());
            				}  catch (IOException e) {
            					e.printStackTrace();
            				} catch (ClassNotFoundException e) {
								e.printStackTrace();
							}
            				
            				if(!dataSet.isEmpty()) {
            					TableView<Airplane> table = new TableView<Airplane>();
                    			TableColumn airlineColumn = new TableColumn("Airline");
                    			airlineColumn.setMinWidth(100);
                    			airlineColumn.setCellValueFactory(
            			                new PropertyValueFactory<Airplane, String>("airline"));
                    			TableColumn departureColumn = new TableColumn("Departure");
                    			departureColumn.setMinWidth(100);
                    			departureColumn.setCellValueFactory(
            			                new PropertyValueFactory<Airplane, String>("departure"));
                    	        TableColumn destinationColumn = new TableColumn("Destination");
                    	        destinationColumn.setMinWidth(100);
                    	        destinationColumn.setCellValueFactory(
            			                new PropertyValueFactory<Airplane, String>("destination"));
                    	        TableColumn dateColumn = new TableColumn("Date");
                    	        dateColumn.setCellValueFactory(
            			                new PropertyValueFactory<Airplane, String>("date"));
                    	        TableColumn timeColumn = new TableColumn("Time");
                    	        timeColumn.setCellValueFactory(
            			                new PropertyValueFactory<Airplane, String>("time"));
                    	        TableColumn priceColumn = new TableColumn("Price");
                    	        priceColumn.setCellValueFactory(
            			                new PropertyValueFactory<Airplane, Integer>("price"));
                    	        TableColumn seatsColumn = new TableColumn("Available Seats");
                    	        seatsColumn.setMinWidth(200);
            			        seatsColumn.setCellValueFactory(
            			                new PropertyValueFactory<Airplane, Integer>("availableSeats"));
            			        
            			        ObservableList<Airplane> dataSetNew = FXCollections.observableArrayList(dataSet);
            			        table.setItems(dataSetNew);
                				table.getColumns().addAll(airlineColumn,departureColumn,destinationColumn,dateColumn,timeColumn,priceColumn,seatsColumn);
                				
                				
                        	      //Creating a Grid Pane 
                        	        GridPane gridPane2 = new GridPane();    
                        	      
                        	        //Setting the vertical and horizontal gaps between the columns 
                        	        gridPane2.setVgap(5); 
                        	        gridPane2.setHgap(5);       
                        	        gridPane2.setPadding(new Insets(10, 10, 10, 10));
                        	        gridPane2.setStyle("-fx-background-color: #DCDCDC;"+
                        	        		"-fx-padding: 10;" +
                        					"-fx-border-style: solid inside;" +
                        					"-fx-border-width: 2;" +
                        					"-fx-border-insets: 5;" +
                        					"-fx-border-radius: 5;" +
                        					"-fx-border-color: #4B0082;");
                        	        
                        	        Button back =new Button("Back");
                        	        back.setCursor(Cursor.HAND);
                        	        back.setOnAction(new EventHandler<ActionEvent>() {
                        	            @Override
                        	            public void handle(ActionEvent event) {
                        	            	Timetable timetable = new Timetable();
                        	            	try {
                        	            		timetable.start(Stage);
                        					} catch (Exception e) {
                        						e.printStackTrace();
                        					}
                        	            	Stage.show();
                        	                
                        	            }

                        	        });
                        	        
                        	        gridPane2.add(table, 0, 1);
                        	        gridPane2.add(back,1,1);
                        	        TimetablePage = new Scene(gridPane2, 1200, 600,Color.GAINSBORO);
                        			window.setScene(TimetablePage);
            				}
            				else {
            					Alert alert = new Alert(AlertType.INFORMATION);
                                alert.setTitle("Warning");
                                alert.setContentText("Sorry, There is no available flight");
                                alert.show();
            				}
            		}
            	}
			}
        	
        });
        
        Button HomePage =new Button("Back to Home Page");
        HomePage.setCursor(Cursor.HAND);
        HomePage.setStyle("-fx-background-color: #B0C4DE");
        HomePage.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
            	HomePage hmp = new HomePage();
            	try {
					hmp.start(window);
				} catch (Exception e) {
					e.printStackTrace();
				}
            	window.show();
                
            }

        });
        URL bookingimg = getClass().getResource("Homepage.jpg");
		String bookingimgUrl = bookingimg.toExternalForm();
        Image bookingimage = new Image(bookingimgUrl);
        // defines a viewport into the source image (achieving a "zoom" effect) and
        // displays it rotated
        ImageView ivbooking = new ImageView();
        ivbooking.setImage(bookingimage);
        ivbooking.setFitWidth(500);
        ivbooking.setFitHeight(500);
        ivbooking.setSmooth(true);
        ivbooking.setCache(true);
        HBox hbox = new HBox();
		GridPane gridPane = new GridPane();
		gridPane.setVgap(5); 
        gridPane.setHgap(5);       
        gridPane.setPadding(new Insets(10, 10, 10, 10));
        gridPane.add(fromText, 0, 0);
        gridPane.add(FromList, 1, 0);
        gridPane.add(ToText, 0, 1);
        gridPane.add(ToList, 1, 1);
        gridPane.add(oneWay, 0, 2);
        gridPane.add(RoundTrip, 1, 2);
        gridPane.add(FromDateCalendar, 0, 3);
        gridPane.add(To2, 1, 3);
        gridPane.add(ToDateCalendar, 2, 3);
        gridPane.add(search, 2, 7);
        gridPane.add(HomePage, 2, 8);
        
        gridPane.setStyle("-fx-padding: 10;" +
				"-fx-border-style: solid inside;" +
				"-fx-border-width: 2;" +
				"-fx-border-insets: 5;" +
				"-fx-border-radius: 5;" +
				"-fx-border-color: #4B0082;"+
				"-fx-background-color: #DCDCDC;");
        
        gridPane.setAlignment(Pos.CENTER);
        hbox.setStyle("-fx-padding: 10;" +
				"-fx-border-style: solid inside;" +
				"-fx-border-width: 2;" +
				"-fx-border-insets: 5;" +
				"-fx-border-radius: 5;" +
				"-fx-border-color: #4B0082;"+
				"-fx-background-color: #DCDCDC;");
        hbox.getChildren().add(gridPane);
        hbox.getChildren().add(ivbooking);
        hbox.setAlignment(Pos.CENTER);
		Group root = new Group(hbox);
        //Creating a scene object 
        Scene scene = new Scene(root, 1200, 620, Color.GAINSBORO); 

        //Setting title to the Stage 
        window.setTitle("Timetable"); 
        
        //Adding scene to the stage
        window.setScene(scene);
        window.setWidth(1200);
        window.setHeight(600);
        //Displaying the contents of the stage 
        window.show();
		
	}
	
	public static void main(String[] args) {
		launch(args);
	}

}
