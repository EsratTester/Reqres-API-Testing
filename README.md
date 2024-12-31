# Introduction

This documentation provides a comprehensive overview of the API testing suite for herokuapp.com , featuring a Postman collection and environment tailored for testing functionalities related to student management. The API enables tasks like retrieving Booking information, creating new Booking, Token,Update Booking,Delete Booking.

# Summary
I have completed an API test of Get Users, Create a User, Get User by ID,Update User, and finally Delete User details https://reqres.in


Within this API testing framework, Booking information is examined, and diverse tests are conducted using various HTTP methods such as POST, GET, DELETE, and PUT.

Summary: A total of 5 Test Scripts and 14 assertions were done. All of them passed  and 0 skipped tests. The number of iteration was 1.

![Screenshot_3](https://github.com/user-attachments/assets/3e3b4e94-172c-4bc2-996c-e2ea3cbc68a9)



# Requirements
Postman
https://www.postman.com/

Node JS
https://nodejs.org/en/

# Details



### Get Users


Pre-Response Scripts
```
var jsonData = pm.response.json()

pm.environment.set("id", jsonData.data[1].id);


pm.test("Validate the status code is 200 ", function(){
    pm.response.to.have.status(200);
})


pm.test("Verify the page value is 2", function(){
    const jsonData = pm.response.json();
   pm.expect(jsonData.page).to.eql(2);

  }) 

pm.test("Validate that all user data contains the fields id, email, first_name, last_name, and avatar", function(){
    const jsonData = pm.response.json().data[0];
    pm.expect(jsonData).to.have.property('id');
    pm.expect(jsonData).to.have.property('email');
    pm.expect(jsonData).to.have.property('first_name');
    pm.expect(jsonData).to.have.property('last_name');
    pm.expect(jsonData).to.have.property('avatar');
});



```
### Create User

Body

```
{
"name": "Tanim",
"job": "Software Engineer"
}

````

Post-response Script

```

pm.test("Validate the status code is 201 ", function(){
    pm.response.to.have.status(201);
})


pm.test("Verify the name and job fields in the response match the request payload", function(){
    var jsonData = pm.response.json();
    pm.expect(jsonData.name).to.eql("Tanim");
    pm.expect(jsonData.job).to.eql("Software Engineer");
});


pm.test("Validate the presence of the id and createdAt fields in the response", function(){
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('id');
    pm.expect(jsonData).to.have.property('createdAt');
});


````


### Get User by ID

**Post-response Script**


````
pm.test("Validate the status code is 200 ", function(){
    pm.response.to.have.status(200);
})


pm.test("Validate that all user data contains the fields id, email, first_name, last_name, and avatar", function(){
    const jsonData = pm.response.json().data;
    pm.expect(jsonData).to.have.property('id');
    pm.expect(jsonData).to.have.property('email');
    pm.expect(jsonData).to.have.property('first_name');
    pm.expect(jsonData).to.have.property('last_name');
    pm.expect(jsonData).to.have.property('avatar');
});
pm.test("Ensure the support section contains valid url and text fields", function(){
    const jsonData = pm.response.json().support;
    pm.expect(jsonData).to.have.property('url');
    pm.expect(jsonData).to.have.property('text');
});

`````


### Update User

 Body
```
{
"name": "Jane Doe",
"job": "Product Manager"
}

```

 Post-response Script
```
pm.test("Validate the status code is 200 ", function(){
    pm.response.to.have.status(200);
})


pm.test("Verify the name and job fields in the response match the request payload", function(){
    var jsonData = pm.response.json();
    pm.expect(jsonData.name).to.eql("Jane Doe");
    pm.expect(jsonData.job).to.eql("Product Manager");
});

pm.test("Validate the presence of the id and createdAt fields in the response", function(){
    const jsonData = pm.response.json();

    pm.expect(jsonData).to.have.property('updatedAt');
});

```




### Delete User

Pre-response Script
```
pm.test("Validate the status code is 200 ", function(){
    pm.response.to.have.status(204);
})



pm.test("Ensure the response body is empty", function () {
    pm.expect(pm.response.text()).to.equal("");
});

```



## Report Configure

**Using Newman**
Newman is a command-line Collection Runner for Postman. It enables you to run and test a Postman Collection directly from the command line.

Install Command
```
npm install -g newman
```
Run Command
- newman run “Path/CollectionName.json” -e Path/EnvironmentName.json
- newman run “Collection Link” -e “Path”/EnvironmentName.json

## Create HTML Report
### Install Command
```
npm install -g newman-reporter-html
```
Or
```
npm install -g newman-reporter-htmlextra
```
### Report Run Command
```
newman run CollectionName.json -e EnvironmentName.json -r html
```
Or
```
newman run CollectionName.json -e EnvironmentName.json -r htmlextra
```
![Reqres-2024-12-31-16-45-55-270-0](https://github.com/user-attachments/assets/574ace7a-781d-4778-a3a4-96543aa721cf)







 
