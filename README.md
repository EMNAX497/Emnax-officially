
// create‑db.js
const sqlite3 = require('sqlite3').verbose();

const db = new sqlite3.Database('emnax.db', err => {
    if (err) throw err;
    console.log('emnax.db opened/created');
});

db.serialize(() => {
    db.run(`
        CREATE TABLE IF NOT EXISTS listings (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            area TEXT NOT NULL,
            min_acres TEXT,
            price_per_acre INTEGER
        )
    `);
    db.run(`
        CREATE TABLE IF NOT EXISTS enquiries (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            name TEXT NOT NULL,
            email TEXT NOT NULL,
            message TEXT NOT NULL,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP
        )
    `);
});

db.close();
