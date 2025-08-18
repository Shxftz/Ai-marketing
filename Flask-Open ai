from flask import Flask, render_template, request
import openai
import os

app = Flask(__name__)

# Set your OpenAI API key
openai.api_key = os.getenv("OPENAI_API_KEY")  # Or replace with your key: "sk-..."

@app.route("/", methods=["GET", "POST"])
def index():
    ad_text = ""
    if request.method == "POST":
        business = request.form["business"]
        product = request.form["product"]
        audience = request.form["audience"]

        prompt = (
            f"Create a short marketing campaign for a business called '{business}' "
            f"that is promoting '{product}' to a target audience of '{audience}'. "
            f"Include a catchy headline, social media caption, and one-line sales pitch."
        )

        try:
            response = openai.Completion.create(
                model="text-davinci-003",
                prompt=prompt,
                max_tokens=200,
                temperature=0.7
            )
            ad_text = response.choices[0].text.strip()
        except Exception as e:
            ad_text = f"Error generating ad: {str(e)}"

    return render_template("index.html", ad_text=ad_text)

if __name__ == "__main__":
    app.run(debug=True)
