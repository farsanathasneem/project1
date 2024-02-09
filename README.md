# project1
import 'dart:io';

class Train {
late  String name;
 late String origin;
 late  String destination;
 late int totalSeats;
 late List<List<bool>> seats;

  Train(this.name,   this.origin , this.destination, this.totalSeats,) {
    seats = List.generate(totalSeats ~/ 10, (index) => List.generate(10, (index) => true));
  }
}

class Booking {
  String userName;
  int trainIndex;
  int row;
  int seat;

  Booking(this.userName, this.trainIndex, this.row, this.seat);
}

class TrainTicketBookingSystem {
   late List<Train> trains;
   late List<Booking> bookings;
   late String origin;
   late String destination;

  TrainTicketBookingSystem() {
    trains = [
      Train("Express Train 1"," cityA ", "City B", 60 ),
      Train("Express Train 1"," cityA ", "City B", 60 ),
    ];
    bookings = [];
  }

  void displayTrains() {
    print("Available Trains:");
    for (int i = 0; i < trains.length; i++) {
      print("$i. ${trains[i].name} - Origin: ${trains[i].origin}, Destination: ${trains[i].destination}, Total Seats: ${trains[i].totalSeats}");
    }
    print("\n");
  }

  void displayAvailableSeats(int trainIndex) {
    print("Available Seats for ${trains[trainIndex].name}:");
    for (int i = 0; i < trains[trainIndex].seats.length; i++) {
      for (int j = 0; j < trains[trainIndex].seats[i].length; j++) {
        if (trains[trainIndex].seats[i][j]) {
          print("Row $i Seat $j");
        }
      }
    }
    print("\n");
  }

  void bookSeat(int trainIndex, String userName, int row, int seat) {
    if (row < 0 || row >= trains[trainIndex].seats.length || seat < 0 || seat >= trains[trainIndex].seats[row].length) {
      print("Invalid seat selection. Please try again.\n");
      return;
    }

    if (trains[trainIndex].seats[row][seat]) {
      trains[trainIndex].seats[row][seat] = false;
      bookings.add(Booking(userName, trainIndex, row, seat));
      print("Seat booked successfully!\n");
    } else {
      print("Seat already booked. Please choose another seat.\n");
    }
  }

  void updateUserInfo(String userName, String newUserName, String newPhoneNumber) {
    for (var booking in bookings) {
      if (booking.userName == userName) {
        booking.userName = newUserName ;
        print("User information updated successfully!\n");
        return;
      }
    }
    print("User not found. Please check the name and try again.\n");
  }

  void displayBookedSeats() {
    print("Booked Seats:");
    for (var booking in bookings) {
      print("${trains[booking.trainIndex].name} - Row ${booking.row} Seat ${booking.seat} booked by ${booking.userName}");
    }
    print("\n");
  }
}

void main() {
  var bookingSystem = TrainTicketBookingSystem();

  while (true) {
    print("1. Display Available Trains");
    print("2. Display Available Seats for a Train");
    print("3. Book a Seat");
    print("4. Update User Information");
    print("5. Display Booked Seats");
    print("6. Exit");

    stdout.write("Enter your choice: ");
    var choice = int.parse(stdin.readLineSync()!);

    switch (choice) {
      case 1:
        bookingSystem.displayTrains();
        break;
      case 2:
        stdout.write("Enter the index of the train: ");
        var trainIndex = int.parse(stdin.readLineSync()!);
        bookingSystem.displayAvailableSeats(trainIndex);
        break;
      case 3:
        stdout.write("Enter your name: ");
        var userName = stdin.readLineSync();
        stdout.write("Enter your  phone number: ");
        var PhoneNumber = stdin.readLineSync();
        stdout.write("Enter the index of the train: ");
        var trainIndex = int.parse(stdin.readLineSync()!);
        stdout.write("Enter the row number: ");
        var row = int.parse(stdin.readLineSync()!);
        stdout.write("Enter the seat number: ");
        var seat = int.parse(stdin.readLineSync()!);

        bookingSystem.bookSeat(trainIndex, userName!, row, seat);
        break;
      case 4:
        stdout.write("Enter your current name: ");
        var currentUserName = stdin.readLineSync();
        stdout.write("Enter your new name: ");
        var newUserName = stdin.readLineSync();
        stdout.write("Enter your new phone number: ");
        var newPhoneNumber = stdin.readLineSync();

        bookingSystem.updateUserInfo(currentUserName!, newUserName!, newPhoneNumber!);
        break;
      case 5:
        bookingSystem.displayBookedSeats();
        break;
      case 6:
        print("Exiting the program. Goodbye!");
        return;
      default:
        print("Invalid choice. Please enter a valid option.\n");
    }
  }
}

ticketbooking
