# Flet + SQLite Crud

1. install Flet:
pip install flet

2. Smile

With Postgresql:

class PostgresContextManager:
    def __enter__(self):
        conn_params = {
            "host": "127.x.x.1",
            "port": 5432,
            "dbname": "test_py",
            "user": "user",
            "password": "pass",
        }
        self.conn = psycopg2.connect(**conn_params)
        self.cur = self.conn.cursor()
        return self.cur

    def __exit__(self, exc_type, exc_value, traceback):
        self.cur.close()
        self.conn.commit()
        self.conn.close()
after you can use 
with PostgresContextManager() as cur:
        cur.execute("SELECT * FROM x WHERE x= %s", (x.value,)) 
and you can print or handle the results using 
        row = cur.fetchone()
        if row is None:
            print("x not found")
        else:
            x = row[0]
