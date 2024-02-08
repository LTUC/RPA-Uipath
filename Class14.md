# Class14 : Robot01_ClothingConsultant

# Problem Domain:
A user enters a city name, the robot then scrapes Google for the temperature and weather in that city, the robot then processes the data and makes a decision which will then suggest a clothing type to the user.


## Will check three casses:

1- Raining. 

2- Too Cold.

3- Too Hot.

4-if the weather is Average.

## Concepts will be applied to this robot:

- Arguments.
- Invoke workflow file.
- flowChart and flow decision.


## Steps:

1- Create two workflows : **Main.xaml and GetWeatherDecision.xaml**.

2- In **Main.xaml** , add **Input Dialog** activity.

   - label : enter a city name.
   - save to : **cityName** (new variable , it's type: string).

3- In **Main.xaml** , invoke this workflow **GetWeatherDecision.xaml**.

4- In **GetWeatherDecision.xaml** , create a new argument **In_cityName** (it's diriction: In , and the type is: string).

5- Go back to **invoke workflow** activity , and import this argument **In_cityName** and the it's value is : **cityName**.

##  In **GetWeatherDecision.xaml** :

6- Add **Use App/Browser** activity.

7- Add **Type Into** activity.

   -"Weather in "+ **In_cityName** +" in Fahrenheit".

8- Add **shortCut** activity and record the **enter** button. 

9- Add **Get Text** activity , and Scrap the temperature degree ,and save to : **Temperature** (new variable and it's type is: string).

10- Add **Get Text** activity , and Scrap the Weather deatils ,and save to : **Weather** (new variable and it's type is: string).

11- Add **FlowChart** after the above sequence.

## In the FlowChart:

12- Add **flow decision** activity "Check if raining".

  #### in properties panel:
  
    - condition field: Weather.tolower.Contains("rain") or Weather.ToLower.Contains("showers") or weather.ToLower.Contains("thunderstorm")
    - displaName field: Check if raining.

  
   #### for True branch:

  - add **Assgin** activity.
     - **OutfitSuggestion** (new variable and it's type is string) = "Bring an umbrella"
     


   #### for False branch:

     - connect it with step 13.

13- Add new **flow decision** activity "Check if too cold".

   #### in properties panel:
   
   - condition field: Convert.ToInt32(Temperature) < 40.
   - displaName field: Check if too cold.

   #### for True branch:

   - add **Assgin** activity.
        - **OutfitSuggestion** = "It is very cold outside.So I recommend wearing a down jacket."


   #### for False branch:

  - connect it with step 14.

14- Add new **flow decision** activity "Check if too hot".

   #### in properties panel:
  
    - condition field: Convert.ToInt32(Temperature)>80.
    - displaName field: Check if too hot.

   #### for True branch:

   - add **Assgin** activity.
        - **OutfitSuggestion** = "It is very hot.Please consider wearing light clothing such as shorts ,skirts or dress."

   #### for False branch:

   - add **Assgin** activity.
        - **OutfitSuggestion** = "The Weather is good .You may want to bring a light jacket, just in case." 
          
   - ***Or*** , add a new **flow decision** activity "if the weather is Average"
     - condition field: Convert.ToInt32(Temperature)>40 and Convert.ToInt32(Temperature)<80 .
     - displaName field: Check if weather is average.
     -  **for True branch**:
          - add **Assgin** activity.
             **OutfitSuggestion** = "The Weather is good ,bring a light jacket if you want." 

15- At the end , after **FlowChart** , add a message box :

    -"The temperature is "+Temperature.ToString+" degrees Fahrenheit. The weather is: "+Weather+". "+OutfitSuggestion.
