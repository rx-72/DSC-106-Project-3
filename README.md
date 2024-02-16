# Investigation of Largest Coal electricity reliance and usage between nations
  We decided to encode our data as points connected by lines with the x-axis representing time (in years, an interval quantity) and the y-axis representing electricity generated (in the natural log of terawatt-hours). Lines made for an effective encoding because they could show how a given country's electricity changed over the years while also allowing for easy comparison between different countries. The points also allowed the visualization to act as a scatterplot to some degree because they can more clearly indicate where exactly a country's energy generation was for a given year. We set all of the points to be small and a pale shade of blue and the lines to be thin and a light shade of grey in order to keep the visualization from being cluttered and allow our interaction feature later on the make particular pieces of data stand out in relation to the rest. We only labeled the x-axis ticks for every five years to keep it from being cluttered and labeled the y-axis ticks for each integer from -5 to 9. Electricity generation differed so significantly between different countries that we decided to apply the natural log to this data so that our y-axis would not be excessively spread out due to most countries never exceeding 100 terawatt-hours but others peaking at well over 1000. Our dataset showed that some countries even had years where they produced 0 terawatt-hours of energy, leading to the natural log of their terawatt-hours for those years being undefined. We decided to visualize these points by setting them at y = -5. We were initially thinking of looking into energy generated through solar power, but its values were even more strung out across the different countries throughout the years and therefore would make for a greater challenge when it came to making the graph visually-appealing.
  
  The y-axis tips are not necessarily easy to interpret the meaning of so we included the original terawatt-hour value along with the country and year in our "tooltip" which appears whenever the cursor hovers near a point. We have this text in black and bold lettering so that it can easily be read over the data points and lines lying beneath it. This helps clear things up especially when it comes to the years where a country produced 0 terawatt-hours of energy and is therefore a the very bottom of the visualization where the y-axis tick is labeled as -5. We also made the line representing the hovered-over country bolder and changed the color from grey to blue to make it stand out from the rest. Similarly, we also changed the point's color from blue to yellow and increased its size to highlight what exactly the data in the tooltip is describing.
  
  We worked separately on various portions of the project until working together throughout the 2/15 lecture which is where most of it was completed. Roughly twenty cumulative people-hours were spent on the assignment with much of it involving debugging issues involving how our data was encoding on the visualization and how it was labeled, especially when it comes to differences between what was seen on our localhost pages and what was presented by the GitHub pages link.
