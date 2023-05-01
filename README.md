Download Link: https://assignmentchef.com/product/solved-eel4712-lab-5
<br>
The objective of this lab is to use a finite state machine integrated with a datapath to calculate the greatest common divisor (GCD) of two numbers, using several different VHDL models.




<strong><em>Required tools and parts:  </em></strong>

Quartus2 software package, ModelSim-Altera Starter Edition, Altera DE10 board.

<strong><em>Pre-lab requirements:  </em></strong>

<ol>

 <li>Study the following pseudo-code to make sure you understand the basic algorithm for calculating the GCD of two numbers. The code has 2 inputs (<em>X</em> and <em>Y</em>), and one output (<em>output</em>). There is also a control input called <em>go</em> and a control output called <em>done</em>.</li>

</ol>

// inputs: go, x, y // outputs: output, done




// reset values (add any others that you might need) output = 0; done = 0;  while(1) {




// wait for go to start circuit  while (go == 0);  done = 0;




// store inputs in registers

tmpX = X;  tmpY = Y;




// main GCD algorithm  while (tmpX != tmpY) {        if (tmpX &lt; tmpY)

tmpY = tmpY-tmpX;       else

tmpX = tmpX-tmpY;

}




// assign output and assert done  output = tmpX;   done = 1;




// make sure go has been cleared before starting again  while (go == 1);

}







<h1>FSMD</h1>

<ol start="2">

 <li>Using the provided GCD entity (gcd.vhd), create a custom circuit that implements the GCD algorithm by using the 1-process FSMD model. <strong>This specification must appear in the FSMD architecture of the GCD entity.</strong> After being reset, the circuit should wait until go becomes 1 (active high), at which point the GCD algorithm should be performed for the given x and y inputs. Upon completion, done should be asserted (active high). <strong>Done should remain asserted until the application is started again, which is represented by a 0 on the go signal followed by a 1. The circuit shouldn’t continuously execute if go is left at 1.</strong></li>

</ol>




Use the provided testbench (gcd_tb.vhd) to test your architecture. Note that the testbench only tests a single architecture. Therefore, make sure the following line:




UUT : entity work.gcd(FSMD)




specifies the FSMD architecture (as shown here). For the other parts of the lab, you will specify a different architecture




<h1>FSM+D1</h1>

<ol start="3">

 <li>In this step, you will implement a custom circuit that implements the GCD algorithm by using the datapath shown below:</li>

</ol>




<strong>Figure 1. FSM+D1 </strong>




Implement the datapath by creating an entity datapath1 (store it in datapath1.vhd). You must use a

structural description that instantiates all of the components shown. Therefore, you will also need a register entity, a 2×1 mux entity, a subtractor entity, and a comparator entity. The register entity must have an enable input that allows/prevents data from being stored. The comparator entity must have a less than output, which connects to the x_lt_y signal, and a not equal output, which connects to the x_ne_y signal. You are free to implement these entities however you like, as long as they have these basic capabilities, and as long as each entity uses a generic for the width.




Next, implement a controller entity called ctrl1 (store it in ctrl1.vhd) that uses the control signals for the illustrated datapath to execute the GCD algorithm. Feel free to use either the 1-process or 2-process FSM model (I highly recommend the 2-process model).




For the provided gcd entity implement the structural architecture (FSM_D1) that connects the controller to the datapath. You must use the FSM_D1 architecture.




Use the provided testbench (gcd_tb.vhd) to test your architecture. Note that the testbench only tests a

single architecture. Therefore, make sure you use the following line for the gcd instantiation:




UUT : entity work.gcd(FSM_D1)

<strong> </strong>

<h1>FSM+D2</h1>

<ol start="4">

 <li>In this step, you will first create a different datapath for the GCD algorithm that only uses a single subtractor. Add any components and/or control signals that are necessary. Call the datapath entity datapath2 and store it in datapath2.vhd. You must use a structural architecture.</li>

</ol>




Next, implement a revised controller entity called ctrl2 (store it in ctrl2.vhd) that is based on the revised datapath. Add any control I/O that is required.




For the provided gcd entity implement the structural architecture (FSM_D2) that connects the new controller to the new datapath. You must use the FSM_D2 architecture.

Use the provided testbench (gcd_tb.vhd) to test your architecture. Note that the testbench only tests a single architecture. Therefore, make sure you use the following line for the gcd instantiation:




UUT : entity work.gcd(FSM_D2)

<strong> </strong>

<h1>Top Level</h1>

<ol start="5">

 <li>Create your own top-level entity top_level, stored in top_level.vhd, that instantiates one of the gcd entities with a width of 8 bits. Since there are only 10 switches, map the lowest 5 bits of the x and y inputs to the switches (the upper 3 bits should be hardcoded to ‘0’). Go and reset are mapped onto buttons (you will need to invert the button for reset), the output is mapped onto the 2 7-segment LEDs (each LED gets 4 bits of the output), and the done signal is mapped onto the decimal point. Make sure to add the 7-segment decoder code to your project. To select a particular architecture for the GCD component, you can either use a configuration or can specify the architecture explicitly:</li>

</ol>




U_GCD : entity work.gcd(FSMD)




See the provided testbench and the top_level entity from lab 3 for examples.




<h1>Extra Credit</h1>

<ol start="6">

 <li>Create a new FSMD (not an FSM+D) architecture for the GCD entity that uses a 2-process model. Note that I have not shown how to do this. The 2-process FSMD is trickier than the 2-process FSM model and the 1-process FSMD model. You will likely run into issues that will test your understanding of VHDL. However, unlike the 1-process FSMD, the 2-process FSMD model has the advantage of not requiring registers on all outputs. Be sure to inform your TA if you are able to get this working.</li>

</ol>




Implement the new FSMD in the FSMD2 architecture for the provided GCD entity.




Use the provided testbench (gcd_tb.vhd) to test your architecture. Note that the testbench only tests a single architecture. Therefore, make sure you use the following line for the gcd instantiation:




UUT : entity work.gcd(FSMD2)




<sup> </sup>Turn in all VHDL. For Step 4, create and submit a diagram illustrating the structure of your revised <sup> </sup>datapath. There must be only one subtractor.







<strong><em>Pre-lab turn in instructions:  </em></strong>

<strong><em> </em></strong>

To submit your pre lab please create a folder that is named your UFID. Inside create another folder P1,P2,P3… for each part that contains the VHDL files for that part. If a report is needed then please include it in the UFID folder. Then zip and upload the folder which is named your UFID.




<strong><em>In-lab procedure (do as much as possible ahead of time):  </em></strong>

<ol>

 <li>Using Quartus, assign pins to each of the top_level.vhd inputs/outputs such that the signals are connected to the appropriate locations on the board.</li>

 <li>Download your design to the board, and test it for different inputs and outputs. Demonstrate the correct functionality for the TA. Make note of the area requirements for the current architecture.</li>

 <li>Demonstrate the other architectures (FSMD, FSM_D1, FSM_D2, FSMD2) to the TA, showing how the area changes. Alternatively, if you do not finish this step, see the lab report section. Note that FSMD2 is extra credit.</li>

 <li><strong>Be prepared to answer simple questions or to make simple extensions that your TA may request. If you have done the pre-lab exercises, these questions should not be difficult. </strong></li>

</ol>

<strong> </strong>

<strong><em>Lab report: (In-lab part only)  </em></strong>

If you had any problems with portions of the lab that could not be resolved during lab, please discuss them along with possible justifications and solutions. Also, if you did not demo all implementations for your TA, create a table that shows how the area requirements differ for each implementation. If you had no problems and demoed all parts during lab, this report is not necessary.


