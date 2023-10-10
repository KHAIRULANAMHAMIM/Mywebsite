import sqlite3

# Create a SQLite database connection and cursor
conn = sqlite3.connect("blog.db")
cursor = conn.cursor()

# Create a table to store blog posts
cursor.execute("""
    CREATE TABLE IF NOT EXISTS posts (
        id INTEGER PRIMARY KEY,
        title TEXT,
        content TEXT
    )
""")
conn.commit()

def create_post():
    title = input("Enter the post title: ")
    content = input("Enter the post content: ")

    cursor.execute("INSERT INTO posts (title, content) VALUES (?, ?)", (title, content))
    conn.commit()
    print("Post created successfully!")

def list_posts():
    cursor.execute("SELECT * FROM posts")
    posts = cursor.fetchall()

    if posts:
        for post in posts:
            print(f"Title: {post[1]}\nContent: {post[2]}\n")
    else:
        print("No posts found.")

while True:
    print("\nBlog Menu:")
    print("1. Create a new post")
    print("2. List all posts")
    print("3. Exit")

    choice = input("Enter your choice: ")

    if choice == "1
