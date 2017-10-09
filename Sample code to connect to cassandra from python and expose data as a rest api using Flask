#!flask/bin/python
from flask import Flask, jsonify
from cassandra.cluster import Cluster


app = Flask(__name__)

cluster = Cluster(['***.**.0.*','**.*.*.**'],port=9042)

session = cluster.connect('samplekeyspace')

tasks =[]
rows = session.execute('SELECT column1,column2  FROM sampletable')
for row in rows:
        tasks.append( {"id": row.column1, "title": row.column2})

@app.route('/todo/api/v1.0/tasks', methods=['GET'])
def get_tasks():
    return jsonify({'tasks': tasks})

if __name__ == '__main__':
    app.run(debug=True)
    
