This template contains placeholders for your experiment's Power On initialization, Experiment tests, and 
provides an empty Associative Lookup Event table. 


LookUp Event Table:

The LookUp event table along with the event actions are located in s2. The Associative Event
Table compares a time value stored in slot 0's program space to the values stored in S2's program memory space
for a match. If there is a match, the event table returns an index number (supplied by the user) to a branch 
instruction which jumps to the label pointed to by the index.  The label contains the set of actions for 
that event. The last instruction of the actions does a "ReturnBack" which returns control to slot 0.

The user must enter the day, hour and minute along with a branch index into the event table's data fields. 
The TAG field should not be touched, it tells the event table whether the event has already been executed 
and not to do it again. The TAG fields must be set to $FF if the event is to execute. 

The supplied code provides 41 event table entries but the event table is set up to look only at the first 11.
The number of entries can easily be expanded to 41 by setting the changing the value in the event table "FOR" 
loop from 10 to 40. If more than 41 entries are needed, the table is easily extended along with the appropriate 
values in the "FOR" loop.

Please note that for debug purposes, the current implementation return the first 11 entries of the 
Event Table whenever there is an event match. This can easily be expanded to show all of the entries. 
Alternatively the display event table can be commented out once the code is proven to reduce screen clutter.


Experiment Test, Calibration, and Initialization:

S1 contains the test, calibration, and setup initialization code for your experiment. The tests enable the
developer to check the functionality of the experiment board. Calibration tests are for capturing timing
and other things needed to establish operating parameters (time, temp, humidity, etc). Finally the setup
initialization code allows the developer to configure the hardware for flight. this includes things like 
filling tubing, pump priming, and other things needed to setup the experiment board for flight operation.

Power On Reset:

S0 contains a placeholder for the Power On pin configuration after power up. It is currently set up to 
alternately flash pin 8 and pin 9. This needs to be replaced with the pin output/input configuration needed 
needed to preventa a conflict between the Experiment's Interface circuits with those of the uLab.

Timing, Heartbeat and McMek Requests:

s0 is the primary timing loop for responding to McMek requests and executing heartbeats every 30s. The clock 
values need to be set up so that the 1s duration time is as close as possible to 1s wallclock time. Setting 
the duration clock comprehends McMek requests and event table actions.The accuracy of this loop is dependent
what code is being executed at the time of the measurement. The RTC and Duration clock are displayed to help
faciliate setting the correct time. S0 also contains the duration day, hour and minute counter used by the
event table in S2.
