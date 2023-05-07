Download Link: https://assignmentchef.com/product/solved-lab-07-object-oriented-programming-cse-021
<br>
<h1>Overview</h1>

This week we are going to be introduced to the Object Oriented Programming (OOP) paradigm. We are going to tackle the problem of creating a Cheese Shop in a new way using OOP. Luckily, we have provided substantial amount of the code for gentle introduction into this new territory. This lab serves as a study guide for OOP and recursion. Recursion occurs when a method calls itself to perform a smaller version of the same task [cf. Sections 12.1 and 12.2]. We use recursion to allow the customer to redo their whole order any number of times. We also implement additional logic that provides the customer a 1% chance of getting their order for free when checking out.




<strong>Before you get started</strong>, read chapters 7.1 – 7.7, and 7.9 if you haven’t already done so. Answer the Assessment questions as you encounter them in the next section. The prompts for answering assessment questions are placed immediately following the material to which the listed questions relate.

<h1>Getting Started</h1>

You should have a Java project in Eclipse titled Lab 21_7. This PDF document is included in the project in the <strong>doc</strong> directory. The Java files you will use in this lab are in the <strong>src</strong> directory.




We start from the simpler version of the shop that only sells the following three fixed types of cheeses <strong>in half-pound packages</strong>:

<ul>

 <li>Humboldt Fog: $25.00 per pound</li>

 <li>Red Hawk: $40.50 per pound</li>

 <li>Teleme: $17.25 per pound</li>

</ul>

When we’re solving problems using OOP, we need to undertake two necessary tasks. The first task is to <strong>define</strong> the class along with its expected behaviors. Second task is to <strong>instantiate</strong> an object of that class type. Usually we can only manipulate an instantiated object of a class.




To create a Cheese Shop, the first thing (object) we need is a shop. So, we define a Shop class which behaves as follows:

<ol>

 <li>List all the cheese types available and the prices</li>

 <li>Asks the user how many pounds of each type of cheese to purchase.

  <ul>

   <li>Validate the input to be &gt;= 0 and to be in 0.5 lb increment for positive amounts.</li>

  </ul></li>

 <li>Calculate Original Sub Total (price*amount of each cheese added together)</li>

 <li>Calculate special discounts based on how many pounds for Humboldt Fog and Red Hawk cheeses the user entered, as well as the total purchase amount o <strong>See Discount Calculation below for details </strong></li>

 <li>Ask the user if they would like to see a list of what they purchased o If yes, a list comes up showing how much of each type of cheese they bought and the cost of each cheese

  <ul>

   <li>Display only the cheese they actually bought</li>

   <li>If no items are purchased, then display a message stating the same (see the Sample Runs below) o If the user answers no, then no itemized information is displayed</li>

  </ul></li>

 <li>Display Original Sub Total, Specials, New Sub Total, Additional Discount and Final Total as shown in the Sample Runs (see Discount Calculation below to see how these are calculated).</li>

</ol>




Shop class will need to have different cheese types and that’s where the Cheese class comes in. Shop will create (<strong>instantiate</strong>) objects of type Cheese to sell to the customers.




We need to <strong>define</strong> the Cheese class whose objects will be used and manipulated by the Shop class. Each cheese has the same basic behavior and state, so we only need to define it once. A cheese has a name, a price and an amount the customer wants to buy. These can be naturally modeled by <em>instance (or member) variables (or fields)</em> declared inside the Cheese class. Then we need to provide member methods in the Cheese class as the primary way to manipulate these variables by other objects, namely of type Shop in our case.




Finally, we need a class with a main method to execute the whole program, and that’s where the RunShop class comes in. This main method will create a shop object of type Shop and call a method called shop.run() to start our Cheese Shop.




<strong>Constructors: </strong>

Each class needs to contain at least one type of constructor (method with the same name as the class) that is called when an object or an instance of the class is created. Everything we have done before is static and you may notice a lack of any constructors. RunShop, for example, does not have a constructor as Java provides one as default. However, when we need a more sophisticated behavior, we need to have specialized constructors.




We have talked briefly about <strong>overloading</strong> but this will be the first time we will utilize it in our labs. The Cheese class will have three different ways of creating an instance using three types of constructors. The difference lies in the parameters each constructor expects that are unique among the three — this way, Java can figure out which one needs to be called depending on the arguments passed during object instantiation. The first Cheese constructor takes no argument, and simply initializes all variables. The second constructor takes the name of a cheese as input, and uses it to initialize the name variable. The third constructor is the most complete, taking the price of a cheese along with its name as inputs.




public Cheese() public Cheese(String name) public Cheese(String name, double price)




[Answer assessment questions 1 and 2]




<strong>Accessors: </strong>

Each cheese type requires three instance variables: name, price and amount. If the shop or any other object wants to know the value of these variables, they should use accessor methods. As this will be the only way to get access, three accessors must be implemented by Cheese. These accessors each contain one return statement, returning the value of one of the three aforementioned variables to the caller.




public String getName() public double getPrice() public int getAmount()




[Answer assessment question 3]

<strong> </strong>

<strong>Mutators: </strong>

Each of the variables in the Cheese class will also need to be set or modified, and that’s where mutators come in. Cheese is a simple class, so there is one mutator method corresponding to each accessor method as seen below:




public void setName(String newName) public void setPrice(double newPrice) public void setAmount(Scanner input)

Your code for validating the input for amount will go into the setAmount() method, so it must be passed the Scanner object to re-request the amount if an invalid one was entered.




[Answer assessment question 4]

<strong>Cheese Class Details: </strong>

Let us look at a simplified version of the Cheese class implementation:




public class Cheese {  private String name;  private double price;

private int amount;




public static int numCheese = 0;




public Cheese() { // Constructor with no parameters   name = “”;   price = 0;   amount = 0;   numCheese++;

}




public Cheese(String name) { // Constructor with name as parameter   this.name = name;   price = 0;   amount = 0;   numCheese++;

}




public String getName() { // Accessor

return name;

}




public void setName(String newName) { // Mutator

name = newName;

}

}




First, we have declared three variables name, price and amount with their appropriate types as instance variables. Instance variables are unique to each instance (object) of the class type. In addition, they are all declared as private so only objects of type Cheese can access their values; otherwise objects of other class types will be able to access the variables directly without going through the accessor methods. We have a public <em>class variable</em> called numCheese that is used to count how many cheese instances have been created. Class variables are shared by all objects of that class type.




[Answer assessment question 5]

<strong> </strong>

<strong> </strong>

<strong>Initialization:  </strong>

It is very important to have a base constructor which initializes all variables to a default value. In our case, we set name to an empty string, price to 0 and amount to 0. We increment the current count of cheese in each constructor so we can keep track of the total number of cheese objects created.




<strong>Variable Resolution: </strong>

The second constructor takes a cheese name as input, and initializes the name variable to the value passed as the argument. However, you may notice that there are two variables called name that this method knows about. First is the instance variable declared in the class, and second is the input parameter to the method. This is a similar situation to overloading where we need to provide a way for Java to differentiate between the two. So, we introduce a way of accessing the implicitly-passed object reference using this [cf. Section 7.11]. Remember everything is an object of some class type now, so we can access the class member (or an object’s instance variable) using this. Thus, we have the following line to appropriately resolve both names and do the correct thing:




this.name = name;




Notice we did not need to use this in the first constructor for any of the variables. We also did not add it to price and amount in the second constructor. It is equally valid to write:




this.name = name; this.price = 0; this.amount = 0;




You may write code as shown above to avoid any confusion about the actual variable being referred to by the code. We provided both ways so you know about each method of accessing variables, and the situations in which they should be used. You will write the third constructor code based on the two examples given above.




[Answer assessment question 6]




<strong>Get and Set Methods: </strong>

getName basically returns name and setName assigns the value of newName to name. These two basic methods need to exist and perform the same function for every member variable of the class. You will need to implement this method pairing for the other two variables. Remember that setAmount() method will need validate the input to be &gt;= 0 and to be in 0.5 lb increment for positive amounts. If an invalid amount is entered, this method will re-request the user for an input (using the Scanner object) until a valid one is obtained.

<h1>Shop class details</h1>

We will step through the code for the Shop class to explain things that are of interest. Two methods, namely printSubTotals and printFinalTotal are unchanged from Lab 04. The discountSpecials method is also nearly identical to Lab 04, except we no longer need any parameters. This is because the amounts and prices of Humboldt Fog and Red Hawk are now available to us using the accessor methods getAmount and getPrice, respectively. The logic for calculating the discount remains the same. A method called printFree has been newly created to emulate behavior when a shop gives everything away for free. Let us begin with the constructor code for Shop which takes no parameters.




Cheese HFog, RHawk, Teleme;




public Shop() {  HFog = new Cheese();

HFog.setName(“Humboldt Fog”);

HFog.setPrice(25.00);




RHawk = new Cheese(“Red Hawk”);

RHawk.setPrice(40.50);




Teleme = new Cheese(“Teleme”, 17.25);

}




You can see that this constructor basically creates 3 instances of cheese using three different constructors. The class contains three instance variables of type Cheese so the member methods can access them freely without having to pass them as parameters. Creating the HFog object calls the empty parameter constructor of Cheese, and the subsequent calls to the two accessors correctly set the instance variables. Creating the RHawk object calls the constructor with the cheese name as input parameter, and only needs one subsequent call to an accessor to set the price. Creating the Teleme object does not need any subsequent calls to accessors since both values are passed in as parameters to the constructor. So, after this we have successfully created all three cheeses that shop is going to sell.




[Answer assessment question 7]




Next, intro needs to ask the amounts for all three cheeses. You will have to add code for RHawk and Teleme. The partial code for this member method is as follows:




private void intro(Scanner input) {

System.out.println(“We sell 3 kinds of Cheese (in 0.5 lb packages):”);

System.out.println(HFog.getName() + “: $” + HFog.getPrice() + ” per pound”);

System.out.println(RHawk.getName() + “: $” + RHawk.getPrice() + ” per pound”);

System.out.println(Teleme.getName() + “: $” + Teleme.getPrice() + ” per pound”);




System.out.print(“
Enter the amount of ” + HFog.getName() + ” in lbs: “);  HFog.setAmount(input);

}




[Answer assessment question 8]




The intro method now takes a Scanner type as a parameter. This avoids the need to create a new object of type Scanner every time intro is called. We pass along this Scanner to the setAmount method where it will be used to get the input from the user. If it is a valid input (&gt;=0 and a multiple of 0.5) then the corresponding cheese object’s amount member variable (HFog in this instance) is set to this input value. Otherwise, your code within setAmount must prompt the user to enter a valid amount as shown in the Sample Runs.




The next method is calcSubTotal that does not need any parameters, since it now knows about the object instance variables (or class members) of type Cheese.




private double calcSubTotal() {  double subTotal = 0;

subTotal += HFog.getAmount() * HFog.getPrice();




return subTotal;

}




[Answer assessment question 9]




calcSubTotal can call each cheese’s amount and price accessors and multiply the returned values to add to the subTotal. The fact that each member of type Cheese simply knows all the information about itself, simplifies the code by using accessor methods. You must add in the rest of the logic so that calcSubTotal returns the correct value.




The code for displaying the list of purchased items is as follows:




private void itemizedList() {  int amt = 0, price = 0;

if ((HFog.getAmount() + RHawk.getAmount() + Teleme.getAmount()) == 0)   System.out.println(“No items were purchased.”);  else {    if ((amt = HFog.getAmount()) &gt; 0) {    price = HFog.getPrice();

System.out.printf(“%.1f lb of %s @ $%.2f = $%.2f
”, amt, HFog.getName(),

price, price*amt);

}

}

}




We use a temporary variables amt and price to store the result of getAmount and getPrice, respectively, so we can avoid calling the method multiple times. The expression amt = HFog.getAmount() assigns the amount of HFog cheese to amt. Then that value is compared against 0 to see if it’s greater. If it is, then we print out the amount of the purchase and cost. This is a small programming trick that can speed up execution because method calls are potentially slow. You can complete the rest of the code to print out the other cheese purchased in similar fashion.




Lastly, we have run() which contains the guts of the program:




public void run() {




Scanner input = new Scanner(System.in);

intro(input);

double subTotal = calcSubTotal();




System.out.println();

System.out.print(“Display the itemized list? (1 for yes): “);  int list = input.nextInt();  if (list == 1)   itemizedList();

int free = (new Random()).nextInt(100);  //System.out.println(“Random num is ” + free);

if (free != 0) {

double newSubTotal = printSubTotals(subTotal, discountSpecials());   printFinalTotal(newSubTotal);

} else {   printFree();

return;

}




System.out.println();

System.out.print(“Do you wish to redo your whole order? (1 for yes): “);  int redo = input.nextInt();




System.out.println();




if (redo == 1)   run();

else

System.out.println(“Thanks for coming!”); }







[Answer assessment question 10]




First thing we do is create a Scanner object called input and use it as an argument in the call to intro.

After we are done with gathering the amounts of cheeses that a customer would like to purchase, we call calcSubTotal() and assign the returned value (the Original Sub Total) to a variable subTotal. Next, we ask the customer if they would like to see an itemized list, and if the input is 1, we call itemizedList, otherwise we proceed to the next step. Now we see the code that provides the customer a 1% chance of getting their order for free. To do so, we generate a random number between 0 and 99, and if it is 0, the customer gets their order for free. Here a trick is used as shown in the following line:




int free = (new Random()).nextInt(100);




The Random class is used to get an integer between 0 – 99. However, since we only use the random number generator object once, we need not store the object in a variable (as we did in Lab 03), as it is not used later. Instead, by using extra set of parentheses, we can tell Java to directly use the object returned and access its method. (new Random()) represents the new object, and nextInt(100) is the method call with input 100.




If the user is not lucky enough to get a free purchase then we display the Original Sub Total, Specials, New Sub Total, Additional Discount and Final Total as we did in Lab 04. Otherwise we call the special printFree method and effectively end the current method’s execution with return;. Even though the return type is void, we can end any method with empty return statement as shown below.




if (free != 0) {

double newSubTotal = printSubTotals(subTotal, discountSpecials());  printFinalTotal(newSubTotal);

} else {  printFree();

return;

}




Finally we ask the user if they want to redo the whole order and if the answer is yes (1), we can just recursively call run() in the if statement shown below.




if (redo == 1)  run();




This way the ordering process keeps going until the user is done or the purchase is free.

<h1>Discount Calculation</h1>

There are two types of discounts offered. The first discount is based on the amounts of Humboldt Fog and Red Hawk bought, with the following specials offered:

<ul>

 <li>Humboldt Fog: Buy 1 package get 1 package free</li>

 <li>Red Hawk: Buy 2 packages get 1 package free</li>

</ul>

Your first discount calculation will remove the cost of free packages (if any) from what the user originally bought. For instance, if the user bought 2 lb of Humboldt Fog (4 packages), then 2 of these packages will be free. And if the user bought 2 lb of Red Hawk (4 packages), then 1 of these packages will be free.




You may think of the technique of calculating the first discount as marking every 2<sup>nd</sup> package as free for Humboldt Fog, and marking every 3<sup>rd</sup> package as free for Red Hawk. In the table below, the blue cells indicate the free Humboldt Fog packages in a 4.5 lb order giving you 4 packages (or 2 lb) for free. Similarly, the orange cells indicate the free Red Hawk packages in a 4.5 lb order giving you 3 packages (or 1.5 lb) for free.




<table width="255">

 <tbody>

  <tr>

   <td colspan="2" width="128"><strong>Humboldt Fog </strong></td>

   <td colspan="2" width="128"><strong>Red Hawk </strong></td>

  </tr>

  <tr>

   <td width="64"><strong>#lb </strong></td>

   <td width="64"><strong>#pkg </strong></td>

   <td width="64"><strong>#lb </strong></td>

   <td width="64"><strong>#pkg </strong></td>

  </tr>

  <tr>

   <td width="64">0</td>

   <td width="64">0</td>

   <td width="64">0</td>

   <td width="64">0</td>

  </tr>

  <tr>

   <td width="64">0.5</td>

   <td width="64">1</td>

   <td width="64">0.5</td>

   <td width="64">1</td>

  </tr>

  <tr>

   <td width="64">1</td>

   <td width="64">2</td>

   <td width="64">1</td>

   <td width="64">2</td>

  </tr>

  <tr>

   <td width="64">1.5</td>

   <td width="64">3</td>

   <td width="64">1.5</td>

   <td width="64">3</td>

  </tr>

  <tr>

   <td width="64">2</td>

   <td width="64">4</td>

   <td width="64">2</td>

   <td width="64">4</td>

  </tr>

  <tr>

   <td width="64">2.5</td>

   <td width="64">5</td>

   <td width="64">2.5</td>

   <td width="64">5</td>

  </tr>

  <tr>

   <td width="64">3</td>

   <td width="64">6</td>

   <td width="64">3</td>

   <td width="64">6</td>

  </tr>

  <tr>

   <td width="64">3.5</td>

   <td width="64">7</td>

   <td width="64">3.5</td>

   <td width="64">7</td>

  </tr>

  <tr>

   <td width="64">4</td>

   <td width="64">8</td>

   <td width="64">4</td>

   <td width="64">8</td>

  </tr>

  <tr>

   <td width="64">4.5</td>

   <td width="64">9</td>

   <td width="64">4.5</td>

   <td width="64">9</td>

  </tr>

 </tbody>

</table>




Thus, the itemized list and discount calculation for a 4.5 lb order of these cheeses will display the following:

Display the itemized list? (1 for yes) 1

4.5 lb of Humboldt Fog @ $25.00 = $112.50

4.5 lb of Red Hawk @ $40.50 = $182.25




Original Sub Total:               $294.75

Specials…

Humboldt Fog (Buy 1 Get 1 Free): -$50.00

Red Hawk (Buy 2 Get 1 Free):     -$60.75 New Sub Total:    $184.00

Here the values are as follows:

<ul>

 <li>Original Sub Total is the price*amount of each cheese added together</li>

 <li>$50 discount for Humboldt Fog corresponds to the 2 lb (or 4 pkgs) in the order that are free</li>

 <li>$60.75 discount for Red Hawk corresponds to the 1.5 lb (or 3 pkgs) in the order that are free</li>

 <li>New Sub Total = Original Sub Total – (Humboldt Fog discount +Red Hawk discount) After obtaining the New Sub Total, the Additional Discount is calculated as follows:</li>

 <li>A 10% discount if New Sub Total is over $150</li>

 <li>An additional 15% discount if New Sub Total is over $250</li>

</ul>

And finally, the Final Total is obtained by subtracting the Additional Discount from the New Sub Total.

<strong> </strong>

<strong>Sample Runs (user input shown in </strong><strong>green</strong><strong>, with each run separated by a dashed-line): </strong>




<table width="671">

 <tbody>

  <tr>

   <td width="671">——————————————————————————-SAMPLE RUN 11   We sell 3 kinds of Cheese (in 0.5 lb packages):2   Humboldt Fog: $25.0 per pound3   Red Hawk: $40.5 per pound4   Teleme: $17.25 per pound56   Enter the amount of Humboldt Fog in lbs: 2.57   Enter the amount of Red Hawk in lbs: 48   Enter the amount of Teleme in lbs: 0910  Display the itemized list? (1 for yes): 111  2.5 lb of Humboldt Fog @ $25.00 = $62.5012  4.0 lb of Red Hawk @ $40.50 = $162.001314       Today is your lucky day!15       2.5 lb of Humboldt Fog @ $0 = $0 16 4.0 lb of Red Hawk @ $0 = $0 17 Total: FREE!!!1819 Ran with Cheese Total: 3</td>

  </tr>

 </tbody>

</table>







<table width="671">

 <tbody>

  <tr>

   <td width="671">——————————————————————————-SAMPLE RUN 21   We sell 3 kinds of Cheese (in 0.5 lb packages):2   Humboldt Fog: $25.0 per pound3   Red Hawk: $40.5 per pound4   Teleme: $17.25 per pound56   Enter the amount of Humboldt Fog in lbs: -27   Invalid input. Enter a value &gt;= 0: 1.38   Invalid input. Enter a value that’s multiple of 0.5: .59   Enter the amount of Red Hawk in lbs: 2.210  Invalid input. Enter a value that’s multiple of 0.5: -511  Invalid input. Enter a value &gt;= 0: 112  Enter the amount of Teleme in lbs: 101314  Display the itemized list? (1 for yes): 115  0.5 lb of Humboldt Fog @ $25.00 = $12.5016  1.0 lb of Red Hawk @ $40.50 = $40.5017  10.0 lb of Teleme @ $17.25 = $172.501819  Original Sub Total:     $225.5020  Specials…21  None      -$0.022  New Sub Total:    $225.5023  Additional 10% Discount:      -$22.5524  Final Total:      $202.952526 Do you wish to redo your whole order? (1 for yes): 12728  We sell 3 kinds of Cheese (in 0.5 lb packages):29  Humboldt Fog: $25.0 per pound30  Red Hawk: $40.5 per pound31  Teleme: $17.25 per pound3233  Enter the amount of Humboldt Fog in lbs: 034  Enter the amount of Red Hawk in lbs: 035  Enter the amount of Teleme in lbs: 03637 Display the itemized list? (1 for yes): 1 38 No items were purchased.3940  Original Sub Total:     $0.0041  Specials…42  None      -$0.043  New Sub Total:    $0.0044  Additional 0% Discount:       -$0.045  Final Total:      $0.004647 Do you wish to redo your whole order? (1 for yes): 04849  Thanks for coming!50  Ran with Cheese Total: 3——————————————————————————-SAMPLE RUN 31   We sell 3 kinds of Cheese (in 0.5 lb packages):2   Humboldt Fog: $25.0 per pound3   Red Hawk: $40.5 per pound4   Teleme: $17.25 per pound56   Enter the amount of Humboldt Fog in lbs: 8.57   Enter the amount of Red Hawk in lbs: 18   Enter the amount of Teleme in lbs: 12.39   Invalid input. Enter a value that’s multiple of 0.5: 12.5</td>

  </tr>

 </tbody>

</table>




<table width="671">

 <tbody>

  <tr>

   <td width="671">10 Display the itemized list? (1 for yes): 0 1112  Original Sub Total:     $468.6313  Specials…14  Humboldt Fog (Buy 1 Get 1 Free): -$100.0015  New Sub Total:    $368.6316  Additional 15% Discount:      -$92.1617  Final Total:      $276.471819 Do you wish to redo your whole order? (1 for yes): 02021  Thanks for coming!22  Ran with Cheese Total: 3——————————————————————————-SAMPLE RUN 41   We sell 3 kinds of Cheese (in 0.5 lb packages):2   Humboldt Fog: $25.0 per pound3   Red Hawk: $40.5 per pound4   Teleme: $17.25 per pound56   Enter the amount of Humboldt Fog in lbs: 4.57   Enter the amount of Red Hawk in lbs: 4.58   Enter the amount of Teleme in lbs: 0910  Display the itemized list? (1 for yes): 111  4.5 lb of Humboldt Fog @ $25.00 = $112.5012  4.5 lb of Red Hawk @ $40.50 = $182.251314  Original Sub Total:     $294.7515  Specials…16  Humboldt Fog (Buy 1 Get 1 Free): -$50.0017  Red Hawk (Buy 2 Get 1 Free): -$60.7518  New Sub Total:    $184.0019  Additional 10% Discount:      -$18.4020  Final Total:      $165.602122 Do you wish to redo your whole order? (1 for yes): 02324  Thanks for coming!25  Ran with Cheese Total: 3</td>

  </tr>

 </tbody>

</table>

<h2>Part 1: Fill-in Shop.java and Cheese.java</h2>

Everywhere you see the comment to “Fill in Code” is where you need to add code to make this program behave correctly. If the comment is to “Fix Code”, you need to change existing code. In most places a sample is provided to help you get started. The program currently runs but the values are obviously incorrect.




main is inside RunShop.java and there is where you should run the whole program.

<strong> </strong>

<h1>Part 2: (Assessment) Logic Check and Level of Understanding</h1>

Create a Word document or text file named Part2 that contains answers to the following:

<ul>

 <li>How can you tell a method is a constructor?</li>

 <li>Would public void cheese() be considered a constructor?</li>

 <li>Does it make sense to have private or void accessor method?</li>

 <li>Would public void setName() be a good mutator declaration?</li>

 <li>How can you tell the difference between instance and class variables?</li>

 <li>Can we write name = name; and what would it mean?</li>

 <li>How can you tell which version of the constructor is being called?</li>

 <li>What does the . operator do for objects?</li>

 <li>Can you use a loop to implement calcSubTotal?</li>

 <li>Can you tell when and where we do the recursion in run()?</li>

 <li>What does this refer to?</li>

 <li>What should be the value of numCheese when RunShop terminates (i.e., the output of the println statement)?</li>

 <li>Give the code to implement public void setName(String name) { … }.</li>

</ul>




<h1>Specification Compliance</h1>

The following are some additional instructions to make sure your project complies with specifications:

<ol>

 <li>Your program must produce an output that <strong>exactly resembles the Sample Output shown above, including identical wording of prompts, spacing, input locations, etc</strong>.</li>

 <li>Your program must ensure the following:

  <ol>

   <li>Your program should not display items that are not bought (amount is 0) when listing them out [cf.</li>

  </ol></li>

</ol>

Sample Run 4, Lines 10-12]. If no items are purchased, then a special message is displayed [cf. Sample Run 2, Line 38].

<ol>

 <li>If no discounts are applied, a special message is displayed [cf. Sample Run 2, Line 21].</li>

</ol>

<ol start="3">

 <li>Your program must check for invalid inputs when entering the amounts [cf. Sample Run 2, Lines 6-12].</li>

 <li>Before you submit, in Eclipse, type CTRL-A (to select everything) followed by a CTRL-I (to fix indentation) on each of your java programs. In MacOS the corresponding keystrokes are Cmd-A followed by Cmd-I.</li>

</ol>

<strong> </strong>