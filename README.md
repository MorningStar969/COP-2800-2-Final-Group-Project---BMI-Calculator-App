# COP-2800-2-Final-Group-Project---BMI-Calculator-App
This is a GitHub repository link for the Final Group Project for IOS App Programming

import SwiftUI

// The main content view of the app that contains the BMI calculator interface, including text fields from height and weight,  calculate button, and a reset button. It also displays the calculated BMI result.
struct ContentView: View {
   @State private var height: String = ""
    @State private var weight: String = ""
    @State private var bmiResult: Double? = nil
    
    func bmiCalculator(height: Double, weight: Double) -> Double {
        return (weight / (height * height)) * 703
    } // This function calculates the BMI based on the given height and weight.
 
    var body: some View {
        ZStack{
            Color.red
            .edgesIgnoringSafeArea(.all)
            VStack {
                Text("BMI Calculator")
                    .font(.system(size: 57))
                    .foregroundColor(.black)
                    .fontWeight(.bold)
                    .padding(.top,40)
                Text("""
                    Underweight: <18.5
                    Normal: 18.5-24.9
                    Overweight: 25-29.9
                    Obese: >30
            """) // This text displays the BMI categories and their corresponding ranges.
                
                .font(.system(size: 27))
                TextField("Enter height in inches", text: $height)
                    .keyboardType(.decimalPad)
                    .foregroundColor(.blue)
                    .textFieldStyle(RoundedBorderTextFieldStyle())
                    .padding()
                // This text field allows the user to enter their height in inches.
                TextField("Enter weight in pounds", text: $weight)
                    .textFieldStyle(RoundedBorderTextFieldStyle())
                    .padding() // This text field allows the user to enter their weight to in pounds.
                Spacer()
                Button(action: {
                    if let heightDouble = Double(height), let weightDouble = Double(weight){
                        bmiResult = bmiCalculator(height: heightDouble, weight: weightDouble)
                    }
                })
                {
                    Text("Calculate").foregroundColor(.white)
                        .padding()
                        .background(Color.blue)
                        .cornerRadius(12)
                } // This button calculates the BMI based on the input height and weight.
                Button (action: {
                height = ""
                weight = ""
                bmiResult = 0.0})
                        {
                            Text("Reset").foregroundColor(Color.white)
                    .padding()
                    .frame(minWidth: 100)
                    .background(Color.gray)
                    .foregroundColor(.white)
                    .cornerRadius(10)}
                .padding(.bottom, 20) // This button resets the input fields and the BMI result.
                if let result = bmiResult{
                    Text("BMI: \(String(format: "%.2f", result))")
                        .font(.system(size: 35))
                        .padding() // This text displays the calculated BMI result.
                }
            }
        }
    }
}
#Preview {
    ContentView() // This is the preview of the main content view of the app.
}
