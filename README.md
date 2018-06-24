Sample Project Description
----------------

This is a sample project to demonstrate git.  My projects will follow this format. All files except this one are blank.

# Loan Price Prediction

In this project, I analyzed data on loans issued through the [LendingClub](https://www.lendingclub.com/) platform.  On the LendingClub platform, potential lenders see some information about potential borrowers, along with an interest rate they'll be paid.  The potential lenders then decide if the interest on the loan is worth the risk of a default (the loan not being repaid), and decide whether to lend to the borrower.  LendingClub publishes anonymous data about its loans and their repayment rates.

Using the data, I analyzed factors that correlated with loans being repaid on time, and did some exploratory visualization and analysis.  I then created a model that predicts the chance that a loan will be repaid given the data surfaced on the LendingClub site.  This model could be useful for potential lenders trying to decide if they should fund a loan.  You can see the exploratory data analysis in the `Exploration.ipynb` notebook above.  You can see the model code and explanations in the `algo` folder.

#Example code with descriptions

def count_performance_rows():
    counts = {}
    with open(os.path.join(settings.PROCESSED_DIR, "Performance.txt"), 'r') as f:
        for i, line in enumerate(f):
            if i == 0:
                continue
            loan_id, date = line.split("|")
            loan_id = int(loan_id)
            if loan_id not in counts:
                counts[loan_id] = {
                    "foreclosure_status": False,
                    "performance_count": 0
                }
            counts[loan_id]["performance_count"] += 1
            if len(date.strip()) > 0:
                counts[loan_id]["foreclosure_status"] = True
    return counts
A better alternative is:

def count_performance_rows():
    """
    A function to count the number of rows that deal with performance for each loan.
    Each row in the source text file is a loan_id and date.
    If there's a date, it means the loan was foreclosed on.
    We'll return a dictionary that indicates if each loan was foreclosed on, along with the number of performance events per loan.
    """

    counts = {}

    # Read the data file.
    with open(os.path.join(settings.PROCESSED_DIR, "Performance.txt"), 'r') as f:
        for i, line in enumerate(f):
            if i == 0:
                # Skip the header row
                continue
            # Each row is a loan id and a date, separated by a |
            loan_id, date = line.split("|")
            # Convert to integer
            loan_id = int(loan_id)
            # Add the loan to the counts dictionary, so we can count the number of performance events.
            if loan_id not in counts:
                counts[loan_id] = {
                    "foreclosure_status": False,
                    "performance_count": 0
                }
            # Increment the counter.
            counts[loan_id]["performance_count"] += 1
            # If there's a date, it indicates that the loan was foreclosed on
            if len(date.strip()) > 0:
                counts[loan_id]["foreclosure_status"] = True
    return counts

Some bullet points with interesting observations you found in exploration
Any interesting charts or diagrams you created
Information about the model, such as algorithm
Error rates and other information about the predictions
Any notes about real-world usage of the model
