Neck Breaker is a small library used for finding bottlenecks in your code.  It is different than a profiler because you can leave it in your code in production and check on it periodically. Think of it as a type of logging api akin to log4j or java.util.logging, but for performance.

==Continuous performance testing==

Neck Breaker allows you to see real world performance results in real production environments. It's very light weight and has a minimal impact on performance.

==Features==

  * Extremely easy to get started and use
  * Prints stats to an Outputter on a regular schedule
  * Output to different mediums (currently only has a ConsoleOutputter, but more to come)
  * Multiple Outputters with different schedules can be used (eg: print to console every 5 minutes and send email every day)
  * Thread safe

==Getting Started==

{{{
// You'll need a scheduled executor, you can make one easily like this if you don't already have one in your program.
ScheduledExecutorService scheduledExecutor = Executors.newSingleThreadScheduledExecutor();

// Create a NeckBreaker object for use throughout your program. 
// Store this in a static field if you'd like for easy access.
NeckBreaker neckBreaker = new NeckBreaker(scheduledExecutor, SECONDS_BETWEEN_PRINTS);

// Now you can wrap any code section with the following blocks.
neckBreaker.start("section1");
// execute some expensive code
neckBreaker.end("section1");
}}}

That's it. Nothing more to it. This will print some performance stats to the console every SECONDS_BETWEEN_PRINTS.

{{{
NeckBreaker Output:
Key	        Count	Avg	Total   Min	Max	
section1	500	1000	500000	650	1621
section2	50	1000	50002	1000	1002
}}}
