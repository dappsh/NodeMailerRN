const nodemailer = require('nodemailer');
const xoauth2 = require('xoauth2');

const express = require('express');
const app = express();

var cors = require('cors')
app.use(cors())

var bodyParser = require('body-parser')
app.use(bodyParser.json());

var transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
        type: 'OAuth2',
        user: 'dwiajengpps@gmail.com',
        clientId: '243655151511-an4o0oa9kbv4k6vorpfvfgbvokier8vt.apps.googleusercontent.com',
        clientSecret: 'BcMresVfHAmEyFV0wLCPaBdZ',
        refreshToken: '1/6xt-Q9tRmpgs2UK5j05quvDv4-ujxwTL4-I4iz7F11U'
    },
    // tls: {
    //     rejectUnauthorized: false
    // }
})

// var mailOptions = {
//     from: 'Tes Node JS <dwiajengpps@gmail.com>',
//     to: 'puspajeng@gmail.com',
//     subject: 'Tes Email NodeJS',
//     text: 'Halo Dunia!',
//     html: '<h1><i>Ini Email ya gaes!</i></h1>'
// }

app.post('/sendemail', (req, res) => {
    var email = req.body.terima
    var subject = req.body.judul
    var messages = req.body.emailpesan
    var mailOptions = {
        to: `${email}`,
        subject: `${subject}`,
        text: `${messages}`,
    }

    transporter.sendMail(mailOptions, (err, res2) => {
        res.send('Email terkirim')
        if (err) {
            console.log('Email failed to send');
            res.send('Email failed to send');
        } else {
            console.log('Email terkirim');
            res.send('Email terkirim!');
        }

        
    })
})

app.listen(3210, () => {
    console.log('Server run @3210')
    
});