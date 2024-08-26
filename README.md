# Environmental-awareness-web 
HackCSB 24 
### Backend (Flask)

1. **Install Flask**: Make sure Flask is installed. You can install it using pip if you haven't already:
   ```bash
   pip install Flask
   ```

2. **Create the Flask App**: Save this code in a file named `app.py`.

   ```python
   from flask import Flask, render_template, request, jsonify

   app = Flask(__name__)

   # Homepage route
   @app.route('/')
   def home():
       return render_template('index.html')

   # Environmental tips route
   @app.route('/tips')
   def tips():
       # Example environmental tips
       tips_list = [
           "Reduce, reuse, and recycle.",
           "Conserve water by turning off the tap while brushing your teeth.",
           "Use energy-efficient appliances.",
           "Plant trees and support reforestation efforts.",
           "Opt for public transportation or carpool to reduce carbon emissions."
       ]
       return jsonify(tips=tips_list)

   if __name__ == '__main__':
       app.run(debug=True)
   ```

### Frontend (HTML)

1. **Create HTML File**: Save this code in a file named `templates/index.html`.

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Environmental Awareness App</title>
       <style>
           body { font-family: Arial, sans-serif; margin: 0; padding: 20px; }
           h1 { color: #2e8b57; }
           button { padding: 10px 20px; margin: 10px 0; cursor: pointer; }
           ul { list-style-type: none; padding: 0; }
           li { margin: 5px 0; }
       </style>
   </head>
   <body>
       <h1>Welcome to the Environmental Awareness App</h1>
       <button onclick="loadTips()">Get Environmental Tips</button>
       <ul id="tipsList"></ul>

       <script>
           function loadTips() {
               fetch('/tips')
                   .then(response => response.json())
                   .then(data => {
                       const tipsList = document.getElementById('tipsList');
                       tipsList.innerHTML = '';
                       data.tips.forEach(tip => {
                           const li = document.createElement('li');
                           li.textContent = tip;
                           tipsList.appendChild(li);
                       });
                   });
           }
       </script>
   </body>
   </html>
   ```
