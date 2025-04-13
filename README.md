Personal Library Manager
📚 Personal Library Manager is a Streamlit-based web app that allows you to manage your personal library. You can add, remove, search, display, and view statistics for your books. The book data is stored in a library.txt file in JSON format, making it easy to load and save your library.

Features
Add a Book: Add new books to your library with details like title, author, year of publication, genre, and read status.

Remove a Book: Select and remove a book from your library.

Search Books: Search for books by title or author.

Display All Books: View all books in your library with filters and sorting options.

Library Statistics: View statistics about your library, such as the total number of books, books you've read, and the percentage of books read.

Technologies Used
Streamlit: Used to build the interactive web app interface.

JSON: For storing and retrieving library data.

OS: For checking if the library.txt file exists.

App Structure
1. Library Loading and Saving
The app reads and saves the book data to a file called library.txt in JSON format. This is done using the following functions:

python
Copy
Edit
def load_library():
    if os.path.exists(FILENAME):
        with open(FILENAME, "r") as file:
            return json.load(file)
    return []

def save_library(library):
    with open(FILENAME, "w") as file:
        json.dump(library, file, indent=4)
2. Session State
To maintain the state of the library data across app reruns, Streamlit’s session_state is used:

python
Copy
Edit
if "library" not in st.session_state:
    st.session_state.library = load_library()
3. Menu System
A sidebar menu is used to navigate between different sections of the app:

python
Copy
Edit
menu = st.sidebar.radio("Menu", [
    "Add a Book", 
    "Remove a Book", 
    "Search Books", 
    "Display All Books", 
    "Statistics"
])
4. Adding a Book
In the Add a Book section, the user can input details such as the title, author, genre, and whether they've read the book. The data is then saved to the library file.

python
Copy
Edit
new_book = {
    "title": title,
    "author": author,
    "year": year,
    "genre": genre,
    "read": read
}
5. Removing a Book
In the Remove a Book section, the user can select a book from the list and remove it. The updated list is saved back to the file.

6. Search for a Book
Users can search for books by either title or author using a search bar. The search is case-insensitive.

python
Copy
Edit
if search_by == "Title":
    results = [b for b in library if query in b["title"].lower()]
7. Display All Books
In the Display All Books section, the user can filter books by genre and read status, and sort them by title, author, or year.

python
Copy
Edit
filtered_books = [book for book in library if book["genre"] == selected_genre]
8. Statistics
In the Statistics section, the app shows the total number of books, the number of books read, and the percentage of books read.

python
Copy
Edit
total = len(library)
read_books = sum(book["read"] for book in library)
percent = (read_books / total) * 100 if total > 0 else 0
9. Custom Footer
A custom footer is added to the app using HTML and inline CSS:

python
Copy
Edit
st.markdown("""
<div style="background-color:#262730; padding:10px; border-radius:10px; margin-top:30px; text-align:center;">
    <span style="color:white;">🚀 Built by <strong>Zeenat Yameen</strong> | 📚 Personal Library Manager</span>
</div>
""", unsafe_allow_html=True)
How to Run
Clone the repository:

bash
Copy
Edit
git clone https://github.com/YOUR_USERNAME/Personal-Library-Manager.git
Install the required dependencies:

bash
Copy
Edit
pip install streamlit
Run the app:

bash
Copy
Edit
streamlit run app.py
License
This project is licensed under the MIT License - see the LICENSE file for details.

# Library_Manager_py
