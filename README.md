
Create virual environement
========================================
    python3 -m ven my_venv
    source my_venv/bin/activate


Create file requirements.txt
========================================

    pip freeze > requirements.txt


Installation
========================================
    pip install fastapi
    pip install "uvicorn[standard]"


Run the server with:
========================================

    uvicorn main:app --reload


Interactive API docs:
========================================
Now go to http://127.0.0.1:8000/docs.
