# Rosie's road co.
An example problem from ASU to make a program that given mileage, road depth, and road width we can determine total materials and total cost of the road.
```
import java.util.Scanner;

public class RosiesRoadCo {
   public static void main(String[] args) {
      Scanner in = new Scanner(System.in);
      
      System.out.print("Enter Road Project Length in Miles : ");
      double miles = in.nextDouble();
      
      System.out.print("Enter Number of Lanes              : ");
      int lanes = in.nextInt();
      
      System.out.print("Enter Depth of Asphalt in Inches   : ");
      int inches = in.nextInt();
      
      System.out.print("Enter Days to Complete Project     : ");
      int days = in.nextInt();
      
      System.out.println();
      
      int truckloads = truckloadsOfAsphalt(miles, lanes, inches);
      int stoplights = numberOfStoplights(miles, lanes);
      int waterPipes = numberOfWaterPipes(miles);
      int powerPipes = numberOfPowerPipes(miles);
      int crew = numberOfCrewMembers(miles, lanes, days);
      
      System.out.print(amountAllocator(truckloads, stoplights, waterPipes, powerPipes, crew));
      
      costCalculator(truckloads, stoplights, waterPipes, powerPipes, crew, days);
      
   }
}
```
Module to figure out the number of stoplights
```
   public static int numberOfStoplights(double miles, int lanes) {
      int stoplightsPerIntersection = 2 + lanes;
      int numberOfIntersections = (int)miles;
      int totalStoplights = stoplightsPerIntersection * numberOfIntersections;
      
      // Then return (not print) that calculated value.
      return totalStoplights;
   }
```
Module to figure out how many truckloads of asphalt you'll need (given each truck can hold 150 tons of asphalt)
```
   public static int truckloadsOfAsphalt(double miles, int lanes, int inches) {
      double roadLength = miles * 5280;
      int roadWidth = lanes * 12;
      double roadDepth = inches / 12.0;.
      double asphaltCubicFeet = roadLength * roadWidth * roadDepth;
      double asphaltPounds = asphaltCubicFeet * 150;
      double approximateTruckLoads = asphaltPounds / 10000;
      int totalTruckloads = (int)Math.ceil(approximateTruckLoads);
      return totalTruckloads;
   }
```
Module to figure out how many power pipes you need to buy give you need to buy them in wholes, and they run 20ft each
```
   public static int numberOfPowerPipes(double miles) {
      double feet = miles * 5280;

      double approximatePowerPipes = feet / 20;

      int totalPowerPipes = (int)Math.ceil(approximatePowerPipes);
      
      return totalPowerPipes;
   }
```
Similar to power pipes, but water pipes run 15ft each
```
   public static int numberOfWaterPipes(double miles) {
      double feet = miles * 5280;

      double approximateWaterPipes = feet / 15;

      int totalWaterPipes = (int)Math.ceil(approximateWaterPipes);
      
      return totalWaterPipes;
   }
```   
Module to figure out how many people you need. the equation ((50.0 * miles * lanes) / days) was given
```
   public static int numberOfCrewMembers(double miles, int lanes, int days) {
      int crewMembers = (int)Math.ceil((50.0 * miles * lanes) / days);
      return crewMembers;
   } 
```
A module that takes the total amount of materials calculated and prints them to console.
```
   public static String amountAllocator(int truckloads, int stoplights, int waterPipes, int powerPipes, int crew) {
      
      String string_0 = "== Amount of Materials Needed ===\n";
      String string_1 = "Truckloads of Asphalt : " + truckloads;
      String string_2 = "\nStoplights            : " + stoplights;
      String string_3 = "\nWater Pipes           : " + waterPipes;
      String string_4 = "\nPower Pipes           : " + powerPipes;
      String string_5 = "\nCrew members needed   : " + crew + "\n";
      
      return string_0 + string_1 + string_2 + string_3 + string_4 + string_5;
   }
```
The final module that takes toal material, and with cost per material given calculates how much in total the project will cost
```
   static void costCalculator (int truckloads, int stoplights, int waterPipes, int powerPipes, int crew, int days) {
      
      double costOfAsphalt = 250 * 5 * truckloads;
      double costOfStoplights = 32000 * stoplights;
      double costOfWaterPipes = 280 * waterPipes;
      double costOfPowerPipes = 350 * powerPipes;
      double costOfLabor = 24.0 * 8.0 * crew * days;
      double totalCost = costOfAsphalt + costOfStoplights + costOfWaterPipes + costOfPowerPipes + costOfLabor;
      
      System.out.println("=== Cost of Materials ============");
      System.out.printf("Cost of Asphalt       : $%.2f\n", costOfAsphalt);
      System.out.printf("Cost of Stoplights    : $%.2f\n", costOfStoplights);
      System.out.printf("Cost of Water pipes   : $%.2f\n", costOfWaterPipes);
      System.out.printf("Cost of Power pipes   : $%.2f\n", costOfPowerPipes);
      System.out.printf("Cost of Labor         : $%.2f\n", costOfLabor);
      System.out.println("=== Total Cost of Project ========");
      System.out.printf("Total cost of project : $%.2f\n", totalCost);
      
   }   
```
