# Import required libraries
from fpdf import FPDF
from flask import Flask, request, render_template, send_file
import os

# Create Flask app
app = Flask(__name__)

# Route for the index page
@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        # Get form data
        company_name = request.form['company_name']
        company_address = request.form['company_address']
        company_phone_number = request.form['company_phone_number']
        company_email = request.form['company_email']
        invoice_number = request.form['invoice_number']
        invoice_date = request.form['invoice_date']
        due_date = request.form['due_date']
        client_name = request.form['client_name']
        client_address = request.form['client_address']
        client_phone_number = request.form['client_phone_number']
        client_email = request.form['client_email']
        total_amount = float(request.form['total_amount'])
        num_installments = int(request.form['num_installments'])
        amount_per_installment = total_amount / num_installments
        total_amount_paid = float(request.form['total_amount_paid'])
        installments_completed = int(request.form['installments_completed'])
        remaining_amount = total_amount - total_amount_paid
        contractor1_name = request.form['contractor1_name']
        pay_rate1 = float(request.form['pay_rate1'])
        contractor2_name = request.form['contractor2_name']
        pay_rate2 = float(request.form['pay_rate2'])
        contractor3_name = request.form['contractor3_name']
        pay_rate3 = float(request.form['pay_rate3'])
        
        # Create PDF object
        pdf = FPDF()
        
        # Add a page
        pdf.add_page()
        
        # Set up fonts
        pdf.set_font("Arial", size=12)
        pdf.set_font("Arial", style="B", size=16)
        
        # Insert company information
        pdf.cell(0, 10, txt=company_name, ln=1, align="C")
        pdf.cell(0, 10, txt=company_address, ln=1, align="C")
        pdf.cell(0, 10, txt=company_phone_number, ln=1, align="C")
        pdf.cell(0, 10, txt=company_email, ln=1, align="C")
        pdf.ln(10)
        
        # Insert invoice information
        pdf.cell(0, 10, txt="Invoice Number: " + invoice_number, ln=1)
        pdf.cell(0, 10, txt="Invoice Date: " + invoice_date, ln=1)
        pdf.cell(0, 10, txt="Due Date: " + due_date, ln=1)
        pdf.ln(10)
        
        # Insert client information
        pdf.cell(0, 10, txt=client_name, ln=1)
        pdf.cell(0, 10, txt=client_address, ln=1)
        pdf.cell(0, 10, txt=client_phone_number, ln=1)
        pdf.cell(0, 10, txt=client_email, ln=1)
        pdf.ln(10)
        
        # Insert installment information
        pdf.cell(0, 10, txt="Total Amount: $" + str(total_amount), ln=1)
        pdf.cell(0, 10, txt="Number of Installments: " + str(num_installments), ln=1)
        pdf.cell(0, 10
