package TravelAgency;

import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.ArrayList;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ServerMain {

   
    public static void main(String[] args) throws Exception {
        try (ServerSocket listener = new ServerSocket(5050)) {
            System.out.println("The server is running...");
            ExecutorService pool = Executors.newFixedThreadPool(100);
            while (listener.isBound()) {
                pool.execute(new Server(listener.accept()));
            }
        }
    }

    private static class Server implements Runnable {
        private Socket socket;
		private ObjectOutputStream out;
		private ObjectInputStream in;
        Server(Socket socket) {
            this.socket = socket;
        }

        @Override
        public void run() {
            System.out.println("Connected: " + socket);
            try (ObjectOutputStream out = new ObjectOutputStream(socket.getOutputStream());
					ObjectInputStream in = new ObjectInputStream(socket.getInputStream())){
				this.out = out;
				this.in=in;
				socket.setTcpNoDelay(true);
                while (true) {
                	String message[] = (String[]) in.readObject();
                    
                    if(message[0].equals("List")) {
                    	ArrayList<User> myList=new ArrayList<>();
                    	myList.addAll((ArrayList<User>)DataBase.userList());
                    	out.writeObject(myList);
                    }
                    if(message[0].equals("TravelList")) {
                    	Traveler tr = (Traveler)DataBase.TravelerTicketInfo(message[1]);
                    	out.writeObject(tr);
                    }
                    if(message[0].equals("login")) {
                    	boolean checkLogin = DataBase.checkPassword(message[1],message[2]);
                    	out.writeObject(checkLogin);
                    }
                    if(message[0].equals("meal")) {
                    	boolean checkTicket = DataBase.checkTicketNumber(message[1]);
                    	out.writeObject(checkTicket);
                    }
                    if(message[0].equals("register")) {
                    	DataBase.NewUser(message[1],message[2],message[3],message[4],message[5],
                    			message[6],message[7],message[8],message[9],message[10],
                    			message[11],message[12],message[13],message[14],message[15],message[16],message[17]);
                    }
                    if(message[0].equals("mealList")) {
                    	DataBase.NewMeal(message[1],message[2]);
                    }
                    
                    if(message[0].equals("OneWayUpdate")) {
                    	DataBase.UpdateSeats(message[1],message[2],message[3],message[4],message[5]);
                    }
                    if(message[0].equals("ReturnUpdate")) {
                    	DataBase.UpdateSeats(message[1],message[2],message[3],message[5],message[7]);
                    	DataBase.UpdateSeats(message[2],message[1],message[4],message[6],message[8]);
                    }
                    if(message[0].equals("checkFlights")) {
                    	ArrayList<Airplane> myList2 = new ArrayList<>();
                    	myList2.addAll((ArrayList<Airplane>)DataBase.checkFlights(message[1],message[2],message[3],message[4],message[5]));
                    	out.writeObject(myList2);
                    }
                    if(message[0].equals("booking")) {
                    	DataBase.NewTraveler(message[1],message[2],message[3],message[4],message[5],
                    			message[6],message[7],message[8],message[9],message[10],
                    			message[11],message[12],message[13],message[14],message[15],message[16],
                    			message[17],message[18],message[19],message[20]);
                    }
                    if(message[0].equals("reset")) {
                    	DataBase.reset(message[1],message[2]);
                    }
                }
            } catch (Exception e) {
                System.out.println(socket);
            } finally {
                try { socket.close(); } catch (IOException e) {}
                System.out.println("Closed: " + socket);
            }
        }
    }
}
