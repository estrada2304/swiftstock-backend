const express = require('express');
const admin = require('firebase-admin');
const app = express();
app.use(express.json());

admin.initializeApp();
const db = admin.firestore();

app.post('/returns', async (req, res) => {
  try {
    const data = req.body;
    await db.collection('returns').add(data);
    res.status(200).send({ message: 'Return saved successfully' });
  } catch (error) {
    console.error(error);
    res.status(500).send({ error: 'Failed to save return' });
  }
});

const PORT = process.env.PORT || 8080;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
