package TravelAgency;


import java.io.IOException;
import java.net.URL;
import java.util.ArrayList;

import javafx.application.Application;
import javafx.beans.property.SimpleObjectProperty;
import javafx.beans.value.ChangeListener;
import javafx.beans.value.ObservableValue;
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
import javafx.scene.control.CheckBox;
import javafx.scene.control.TableColumn;
import javafx.scene.control.TableView;
import javafx.scene.control.Alert.AlertType;
import javafx.scene.control.cell.PropertyValueFactory;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.scene.layout.BorderPane;
import javafx.scene.layout.GridPane;
import javafx.scene.layout.HBox;
import javafx.scene.layout.VBox;
import javafx.scene.paint.Color;
import javafx.scene.text.Font;
import javafx.scene.text.Text;
import javafx.scene.control.TextField;
import javafx.stage.Stage;
import javafx.util.Callback;

public class OrderMeal extends Application{
	private ArrayList<Meal> ShoppingList =new ArrayList<>();
	private String NumberOfTicket="";
	private Text YourList = new Text("Your Shopping List");
	private TableView<Meal> Mealtable = new TableView<Meal>();
	private Button delete = new Button("Delete");
	private Button ConfirmList = new Button("Confirm Your Shopping List");
	private Scene PaymentPage;
	private double TotalMealPrice=0;
	@Override
	public void start(Stage stage) throws Exception {
		YourList.setVisible(false);
		delete.setVisible(false);
		ConfirmList.setVisible(false);
		GridPane Shop =new GridPane(); 
		Shop.setVisible(false);
		Font myFont = new Font("Segoe Print", 15);
		Font myFont2 = new Font("Segoe Print", 40);
		Text orderText = new Text("Order your special meal");
		YourList.setFont(myFont);
		orderText.setFont(myFont2);
		Text ticketNOText = new Text("Please enter your ticket number:");
		ticketNOText.setFont(myFont);
		TextField ticketNOTextField = new TextField();
		Alert WarningAlert = new Alert(AlertType.INFORMATION);
		WarningAlert.setTitle("Confirmation");
		Image image = new Image(getClass().getResourceAsStream("steak.jpg"),100,100,false,false);
		
		ImageView imgview = new ImageView(image);
		imgview.maxWidth(50);
		imgview.maxHeight(50);
        Button steakButton = new Button();
        steakButton.setMaxSize(50,50);
        steakButton.setGraphic(imgview);
        steakButton.setVisible(false);
        Text steakPrice = new Text("Steak "+"25 \u00A3");
        steakPrice.setFont(myFont);
        steakPrice.setVisible(false);
        steakButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override public void handle(ActionEvent e) {
            	WarningAlert.setContentText("This meal is added to your shopping cart");
				WarningAlert.show();
				Meal steak = new Meal("Steak",25);
				ShoppingList.add(steak);
            }
        });
        
        Image chickenImage = new Image(getClass().getResourceAsStream("chickenNugget.jpg"),100,100,false,false);
        ImageView imgview2 = new ImageView(chickenImage);
		imgview2.maxWidth(30);
		imgview2.maxHeight(30);
        Button chickenButton = new Button();
        chickenButton.setMaxSize(30, 30);
        chickenButton.setGraphic(imgview2);
        chickenButton.setMaxSize(50, 50);
        chickenButton.setVisible(false);
        Text chickenPrice = new Text("Chicken nuggets "+"15 \u00A3");
        chickenPrice.setFont(myFont);
        chickenPrice.setVisible(false);
        chickenButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override public void handle(ActionEvent e) {
            	WarningAlert.setContentText("This meal is added to your shopping cart");
				WarningAlert.show();
				Meal chicken = new Meal("Chicken",15);
				ShoppingList.add(chicken);
            }
        });
        
        Image fishImage = new Image(getClass().getResourceAsStream("fishFillet.jpg"),100,100,false,false);
        ImageView imgview3 = new ImageView(fishImage);
		imgview3.maxWidth(30);
		imgview3.maxHeight(30);
        Button fishButton = new Button();
        fishButton.setMaxSize(30, 30);
        fishButton.setGraphic(imgview3);
        fishButton.setMaxSize(50, 50);
        fishButton.setVisible(false);
        Text fishkPrice = new Text("Fish Fillet "+"17.5 \u00A3");
        fishkPrice.setFont(myFont);
        fishkPrice.setVisible(false);
        fishButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override public void handle(ActionEvent e) {
            	WarningAlert.setContentText("This meal is added to your shopping cart");
				WarningAlert.show();
				Meal fish = new Meal("Fish",17.5);
				ShoppingList.add(fish);
            }
        });
		
        Image PizzaImage = new Image(getClass().getResourceAsStream("pizza.jpg"),100,100,false,false);
        ImageView imgview4 = new ImageView(PizzaImage);
		imgview4.maxWidth(30);
		imgview4.maxHeight(30);
        Button pizzaButton = new Button();
        pizzaButton.setMaxSize(30, 30);
        pizzaButton.setGraphic(imgview4);
        pizzaButton.setMaxSize(50, 50);
        pizzaButton.setVisible(false);
        Text pizzaPrice = new Text("Pizza "+"13 \u00A3");
        pizzaPrice.setVisible(false);
        pizzaPrice.setFont(myFont);
        pizzaButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override public void handle(ActionEvent e) {
            	WarningAlert.setContentText("This meal is added to your shopping cart");
				WarningAlert.show();
				Meal pizza = new Meal("Pizza",13);
				ShoppingList.add(pizza);
            }
        });
        
        HBox hbox = new HBox(50);
        HBox hbox5 = new HBox(50);
        hbox.getChildren().add(steakButton);
        hbox5.getChildren().add(steakPrice);
        hbox.getChildren().add(chickenButton);
        hbox5.getChildren().add(chickenPrice);
        hbox.getChildren().add(fishButton);
        hbox5.getChildren().add(fishkPrice);
        hbox.getChildren().add(pizzaButton);
        hbox5.getChildren().add(pizzaPrice);
        
        
        Image hamburgerImage = new Image(getClass().getResourceAsStream("hamburger.jpg"),100,100,false,false);
        ImageView imgview5 = new ImageView(hamburgerImage);
		imgview5.maxWidth(30);
		imgview5.maxHeight(30);
        Button hamburgerButton = new Button();
        hamburgerButton.setMaxSize(30, 30);
        hamburgerButton.setGraphic(imgview5);
        hamburgerButton.setMaxSize(50, 50);
        hamburgerButton.setVisible(false);
        Text hamburgerPrice = new Text("Hamburger " +"10.25 \u00A3");
        hamburgerPrice.setFont(myFont);
        hamburgerPrice.setVisible(false);
        hamburgerButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override public void handle(ActionEvent e) {
            	WarningAlert.setContentText("This meal is added to your shopping cart");
				WarningAlert.show();
				Meal ham = new Meal("Hamburger",10.25);
				ShoppingList.add(ham);
            }
        });
        
        Image soupImage = new Image(getClass().getResourceAsStream("soup.jpg"),100,100,false,false);
        ImageView imgview6 = new ImageView(soupImage);
		imgview6.maxWidth(30);
		imgview6.maxHeight(30);
        Button soupButton = new Button();
        soupButton.setMaxSize(30, 30);
        soupButton.setGraphic(imgview6);
        soupButton.setMaxSize(50, 50);
        soupButton.setVisible(false);
        Text soupPrice = new Text("Soup "+"8 \u00A3");
        soupPrice.setFont(myFont);
        soupPrice.setVisible(false);
        soupButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override public void handle(ActionEvent e) {
            	WarningAlert.setContentText("This meal is added to your shopping cart");
				WarningAlert.show();
				Meal soup = new Meal("Soup",8);
				ShoppingList.add(soup);
            }
        });
		
        Image latteImage = new Image(getClass().getResourceAsStream("latte.jpg"),100,100,false,false);
        ImageView imgview7 = new ImageView(latteImage);
		imgview7.maxWidth(30);
		imgview7.maxHeight(30);
        Button latteButton = new Button();
        latteButton.setMaxSize(30, 30);
        latteButton.setGraphic(imgview7);
        latteButton.setMaxSize(50, 50);
        latteButton.setVisible(false);
        Text lattePrice = new Text("Coffee Latte "+ "5.30 \u00A3");
        lattePrice.setFont(myFont);
        lattePrice.setVisible(false);
        latteButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override public void handle(ActionEvent e) {
            	WarningAlert.setContentText("This meal is added to your shopping cart");
				WarningAlert.show();
				Meal latte = new Meal("Latte",5.30);
				ShoppingList.add(latte);
            }
        });
        
        Image cokeImage = new Image(getClass().getResourceAsStream("coke.jpg"),100,100,false,false);
        ImageView imgview8 = new ImageView(cokeImage);
		imgview8.maxWidth(30);
		imgview8.maxHeight(30);
        Button cokeButton = new Button();
        cokeButton.setMaxSize(30, 30);
        cokeButton.setGraphic(imgview8);
        cokeButton.setMaxSize(50, 50);
        cokeButton.setVisible(false);
        Text cokePrice = new Text("Coke "+"4 \u00A3");
        cokePrice.setFont(myFont);
        cokePrice.setVisible(false);
        cokeButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override public void handle(ActionEvent e) {
            	WarningAlert.setContentText("This meal is added to your shopping cart");
				WarningAlert.show();
				Meal coke = new Meal("Coke",4);
				ShoppingList.add(coke);
            }
        });
        
        HBox hbox2 = new HBox(50);
        HBox hbox6 = new HBox(50);
        
        hbox2.getChildren().add(hamburgerButton);
        hbox6.getChildren().add(hamburgerPrice);
        hbox2.getChildren().add(soupButton);
        hbox6.getChildren().add(soupPrice);
        hbox2.getChildren().add(latteButton);
        hbox6.getChildren().add(lattePrice);
        hbox2.getChildren().add(cokeButton);
        hbox6.getChildren().add(cokePrice);
        
        
        
        Image orangeJuiceImage = new Image(getClass().getResourceAsStream("orangeJuice.jpg"),100,100,false,false);
        ImageView imgview9 = new ImageView(orangeJuiceImage);
		imgview9.maxWidth(30);
		imgview9.maxHeight(30);
        Button orangeJuiceButton = new Button();
        orangeJuiceButton.setMaxSize(30, 30);
        orangeJuiceButton.setGraphic(imgview9);
        orangeJuiceButton.setMaxSize(50, 50);
        orangeJuiceButton.setVisible(false);
        Text orangeJuicePrice = new Text("Orange Juice "+"10.25 \u00A3");
        orangeJuicePrice.setFont(myFont);
        orangeJuicePrice.setVisible(false);
        orangeJuiceButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override public void handle(ActionEvent e) {
            	WarningAlert.setContentText("This meal is added to your shopping cart");
				WarningAlert.show();
				Meal Ojuice = new Meal("Orange juice",10.25);
				ShoppingList.add(Ojuice);
            }
        });

        Image appleJuiceImage = new Image(getClass().getResourceAsStream("apple_juice.jpeg"),100,100,false,false);
        ImageView imgview10 = new ImageView(appleJuiceImage);
		imgview10.maxWidth(30);
		imgview10.maxHeight(30);
        Button appleJuiceButton = new Button();
        appleJuiceButton.setMaxSize(30, 30);
        appleJuiceButton.setGraphic(imgview10);
        appleJuiceButton.setMaxSize(50, 50);
        appleJuiceButton.setVisible(false);
        Text appleJuicePrice = new Text("Apple Juice "+"10.25 \u00A3");
        appleJuicePrice.setFont(myFont);
        appleJuicePrice.setVisible(false);
        appleJuiceButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override public void handle(ActionEvent e) {
            	WarningAlert.setContentText("This meal is added to your shopping cart");
				WarningAlert.show();
				Meal Ajuice = new Meal("Apple juice",10.25);
				ShoppingList.add(Ajuice);
            }
        });
        
        Image chocImage = new Image(getClass().getResourceAsStream("choc.jpg"),100,100,false,false);
        ImageView imgview11 = new ImageView(chocImage);
		imgview11.maxWidth(30);
		imgview11.maxHeight(30);
        Button chocButton = new Button();
        chocButton.setMaxSize(30, 30);
        chocButton.setGraphic(imgview11);
        chocButton.setMaxSize(50, 50);
        chocButton.setVisible(false);
        Text chocPrice = new Text("Chocolate Cake "+"3 \u00A3");
        chocPrice.setFont(myFont);
        chocPrice.setVisible(false);
        chocButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override public void handle(ActionEvent e) {
            	WarningAlert.setContentText("This meal is added to your shopping cart");
				WarningAlert.show();
				Meal ChocolateCake = new Meal("Chocolate Cake",3);
				ShoppingList.add(ChocolateCake);
            }
        });
        
        Image strawberryCakeImage = new Image(getClass().getResourceAsStream("strawberryCake.jpg"),100,100,false,false);
        ImageView imgview12 = new ImageView(strawberryCakeImage);
		imgview12.maxWidth(30);
		imgview12.maxHeight(30);
        Button strawberryCakeButton = new Button();
        strawberryCakeButton.setMaxSize(30, 30);
        strawberryCakeButton.setGraphic(imgview12);
        strawberryCakeButton.setMaxSize(50, 50);
        strawberryCakeButton.setVisible(false);
        Text strawberryCakePrice = new Text("Strawberry Cake "+"6.40 \u00A3");
        strawberryCakePrice.setFont(myFont);
        strawberryCakePrice.setVisible(false);
        strawberryCakeButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override public void handle(ActionEvent e) {
            	WarningAlert.setContentText("This meal is added to your shopping cart");
				WarningAlert.show();
				Meal StrawberryCake = new Meal("Strawberry Cake",6.40);
				ShoppingList.add(StrawberryCake);
            }
        });
		
        
        HBox hbox4 = new HBox(50);
        HBox hbox8 = new HBox(50);
        hbox4.getChildren().add(orangeJuiceButton);
        hbox8.getChildren().add(orangeJuicePrice);
        hbox4.getChildren().add(appleJuiceButton);
        hbox8.getChildren().add(appleJuicePrice);
        hbox4.getChildren().add(chocButton);
        hbox8.getChildren().add(chocPrice);
        hbox4.getChildren().add(strawberryCakeButton);
        hbox8.getChildren().add(strawberryCakePrice);
        
        Button  ShoppingCart=new Button("Confirm");
        ShoppingCart.setCursor(Cursor.HAND);
        ShoppingCart.setVisible(false);
        ShoppingCart.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
            	Shop.setVisible(true);
            	ConfirmList.setVisible(true);
            	delete.setVisible(true);
            	YourList.setVisible(true);
    			TableColumn MealColumn = new TableColumn("Meal");
    			MealColumn.setMinWidth(100);
    			MealColumn.setCellValueFactory(
		                new PropertyValueFactory<Meal, String>("MealName"));
    			TableColumn ChooseColumn = new TableColumn("Choose");
    			ChooseColumn.setMinWidth(200);
    			ChooseColumn.setCellValueFactory(new Callback<TableColumn.CellDataFeatures<Meal, CheckBox>, ObservableValue<CheckBox>>() {

		            @Override
		            public ObservableValue<CheckBox> call(
		                    TableColumn.CellDataFeatures<Meal, CheckBox> box) {
		                Meal user = box.getValue();

		                CheckBox checkBox = new CheckBox();

		                checkBox.selectedProperty().setValue(user.isSelect());

		                checkBox.selectedProperty().addListener(new ChangeListener<Boolean>() {
		                    public void changed(ObservableValue<? extends Boolean> ov,
		                            Boolean old_val, Boolean new_val) {

		                        user.setSelect(new_val);

		                    }
		                });

		                return new SimpleObjectProperty<CheckBox>(checkBox);

		            }

		        });
		        
		        ObservableList<Meal> OurData = FXCollections.observableArrayList(ShoppingList);
		        Mealtable.setItems(OurData);
				Mealtable.getColumns().addAll(MealColumn,ChooseColumn);
				
				
				
		        delete.setOnAction(new EventHandler<ActionEvent>() {
		            @Override
		            public void handle(ActionEvent event) {
		            	ObservableList<Meal> selectMeals = FXCollections.observableArrayList();
    	            	
    	        		for(Meal m: OurData) {
    	        			if(m.isSelect()) {
    	        			selectMeals.add(m);
    	 
    	        			}
    	        		}
    	        		OurData.removeAll(selectMeals);
    	        		Mealtable.refresh();
    	        		 Mealtable.setItems(OurData);
    	        		 
		            }

		        });
		        
		        ConfirmList.setOnAction(new EventHandler<ActionEvent>() {
		            @Override
		            public void handle(ActionEvent event) {
		            	ObservableList<Meal> FinalselectMeals = FXCollections.observableArrayList();
		            	for(Meal m: OurData) {
    	        			if(m.isSelect()) {
    	        			FinalselectMeals.add(m);
    	 
    	        			}
    	        		}
		            	Font myFont = new Font("Segoe Print", 20);
    	        		Text bank = new Text("Welcome to the \"Safest\" Bank");
    	        		bank.setStyle("-fx-background-color: #708090");
    	        		bank.setFont(myFont);
    	        		Text CardNumberText = new Text("Card Number:");
    	        		Text CvvText = new Text("CVV:");
    	        		Text CardNameText = new Text("Card holder's name:");
    	        		TextField CardNumberTextField = new TextField();
    	                TextField CvvTextField = new TextField();
    	                TextField CardNameTextField = new TextField();
    	                
    	                for (int f=0;f<FinalselectMeals.size();f++) {
    	                	TotalMealPrice += FinalselectMeals.get(f).getMealprice();
    	                }
    	                Text TotalPriceText = new Text("Total price: "+ TotalMealPrice);
     	               TotalPriceText.setFont(myFont);
     	               
     	               URL myImg = getClass().getResource("emoji.png");
     	       			String myImgUrl = myImg.toExternalForm();
     	               Image myImage = new Image(myImgUrl);
     	               ImageView MyImgView = new ImageView();
     	               MyImgView.setImage(myImage);
     	               
     	              Button ConfirmPayment =new Button("Confirm");
     	             ConfirmPayment.setCursor(Cursor.HAND);
     	            ConfirmPayment.setStyle("-fx-background-color: #B0C4DE");
     	           ConfirmPayment.setOnAction(new EventHandler<ActionEvent>() {
       	                 @Override
       	                 public void handle(ActionEvent event) {
       	                	if(CardNumberTextField.getText().equals("")||CvvTextField.getText().equals("")||CardNameTextField.getText().equals("") ) {
           	            		Alert EmptyFieldAlert2 = new Alert(AlertType.INFORMATION);
           	            		EmptyFieldAlert2.setTitle("Warning");
           	            		EmptyFieldAlert2.setContentText("Please fill out all the blanks");
           	            		EmptyFieldAlert2.show();
           	            	}
       	                	else {
       	                		if(TotalMealPrice==0) {
       	                			Alert NothingAlert = new Alert(AlertType.CONFIRMATION);
       	                			NothingAlert.setTitle("Confirmation");
       	                			NothingAlert.setContentText("You didn't choose any meal");
       	                			NothingAlert.show();
           	                		HomePageRegisteredUsers back2 = new HomePageRegisteredUsers();
                  	                 try {
           	     	            		back2.start(stage);
           	     					} catch (Exception e) {
           	     						e.printStackTrace();
           	     					}
           	     	            	stage.show();
       	                		}
       	                	else {
       	                		String FinalMeals="";
       	                		for (int fm=0;fm<OurData.size();fm++) {
       	                			FinalMeals =FinalMeals+ OurData.get(fm).getMealName() +" ";
       	                		}
       	                		
       	                		try {
       	             			String [] entities= {"mealList",FinalMeals,NumberOfTicket};
       	             			HomePage.dos.writeObject(entities);
       	             		} catch (IOException e) {
       	             			e.printStackTrace();
       	             		}
       	                		
       	                		
       	                		Alert MealConfirmationAlert = new Alert(AlertType.CONFIRMATION);
       	                		MealConfirmationAlert.setTitle("Confirmation");
       	                		MealConfirmationAlert.setContentText("Your Special meal is added successfully");
       	                		MealConfirmationAlert.show();
       	                		HomePageRegisteredUsers back = new HomePageRegisteredUsers();
              	                 try {
       	     	            		back.start(stage);
       	     					} catch (Exception e) {
       	     						e.printStackTrace();
       	     					}
       	     	            	stage.show();
       	                	}
       	                	}
       	                 }

       	             });
     	               
     	              GridPane grid2 = new GridPane();
     	              grid2.add(bank, 0, 0);
     	              grid2.add(MyImgView, 1, 0);
     	              grid2.add(CardNumberText, 0, 1);
     	              grid2.add(CardNumberTextField, 1, 1);
     	              grid2.add(CvvText, 0, 2);
     	              grid2.add(CvvTextField, 1, 2);
     	              grid2.add(CardNameText, 0, 3);
     	              grid2.add(CardNameTextField, 1, 3);
     	              grid2.add(TotalPriceText, 0, 4);
     	              grid2.add(ConfirmPayment, 0, 5);
     	              grid2.setAlignment(Pos.CENTER);
   	               
   	        		PaymentPage = new Scene(grid2, 1200, 600,Color.GAINSBORO);
           			stage.setScene(PaymentPage);
		            }

		        });
				
		        Shop.add(YourList,4,0);
		        Shop.add(Mealtable,4,1);
		        Shop.add(ConfirmList,4,2);
		        Shop.add(delete,5,2);
            }

        });
        
        Button  FlightNumberButton=new Button("OK");
        FlightNumberButton.setCursor(Cursor.HAND);
        FlightNumberButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
            	boolean checkTicketNum =false;
            	Alert WarningAlertTicket = new Alert(AlertType.ERROR);
            	WarningAlertTicket.setTitle("Warning!");
        		NumberOfTicket = ticketNOTextField.getText();
        		if(NumberOfTicket.equals("")) {
        			WarningAlertTicket.setContentText("Please Enter Your Ticket Number");
        			WarningAlertTicket.show();
        		}
        		else {
        			String [] OrderMealInputs= {"meal",NumberOfTicket};
                	try {
        				HomePage.dos.writeObject(OrderMealInputs);
        				checkTicketNum = (boolean) HomePage.dis.readObject();
        			} catch (ClassNotFoundException e1) {
        				e1.printStackTrace();
        			} catch (IOException e1) {
        				e1.printStackTrace();
        			}
                	if(checkTicketNum==false) {
                		Alert WarningAlertWrongTicketNumber = new Alert(AlertType.ERROR);
                		WarningAlertWrongTicketNumber.setTitle("Warning!");
                		WarningAlertWrongTicketNumber.setContentText("Sorry, You didn't book any flights");
                		WarningAlertWrongTicketNumber.show();
                	}
                	else {
                		steakButton.setVisible(true);
                        steakPrice.setVisible(true);
                        chickenButton.setVisible(true);
                        chickenPrice.setVisible(true);
                        fishButton.setVisible(true);
                        fishkPrice.setVisible(true);
                        pizzaButton.setVisible(true);
                        pizzaPrice.setVisible(true);
                        hamburgerButton.setVisible(true);
                        hamburgerPrice.setVisible(true);
                        soupButton.setVisible(true);
                        soupPrice.setVisible(true);
                        latteButton.setVisible(true);
                        lattePrice.setVisible(true);
                        cokeButton.setVisible(true);
                        cokePrice.setVisible(true);
                        orangeJuiceButton.setVisible(true);
                        orangeJuicePrice.setVisible(true);
                        appleJuiceButton.setVisible(true);
                        appleJuicePrice.setVisible(true);
                        chocButton.setVisible(true);
                        chocPrice.setVisible(true);
                        strawberryCakeButton.setVisible(true);
                        strawberryCakePrice.setVisible(true);
                        ShoppingCart.setVisible(true);
                	}
        		}
            }

        });
        VBox vbox = new VBox();
        vbox.getChildren().add(FlightNumberButton);
        
        GridPane grid = new GridPane();
        grid.setVgap(5); 
        grid.setHgap(5);       
        grid.setPadding(new Insets(10, 10, 10, 10));
        grid.add(ticketNOText, 0, 0);
        grid.add(ticketNOTextField, 1, 0);
        grid.add(FlightNumberButton, 2, 0);
        grid.add(Shop, 3, 0);
        grid.add(orderText, 0, 1);
        
        grid.add(hbox, 0, 2);
        grid.add(hbox5, 0, 3);
        grid.add(hbox2, 0, 4);
        grid.add(hbox6, 0, 5);
        grid.add(hbox4, 0, 6);
        grid.add(hbox8, 0, 7);
        grid.add(ShoppingCart, 1, 7);
        grid.setStyle("-fx-background-color: #DCDCDC;"+
        		"-fx-padding: 10;" +
				"-fx-border-style: solid inside;" +
				"-fx-border-width: 2;" +
				"-fx-border-insets: 5;" +
				"-fx-border-radius: 5;" +
				"-fx-border-color: #4B0082;");
        grid.setAlignment(Pos.CENTER);
        BorderPane myborder = new BorderPane();
        myborder.setLeft(grid);
        myborder.setRight(Shop);
        Scene scene = new Scene(myborder, 1500, 600, Color.GAINSBORO); 
        
        //Setting title to the Stage 
        stage.setTitle("Your Special Meal"); 
        //Adding scene to the stage 
        stage.setScene(scene);
        //Displaying the contents of the stage 
        stage.show();
	}

}
