# CLI-Employee-Management-System-Using-Node.js-and-Arrays
const readline = require('readline');
let employees = [];
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});
function showMenu() {
    console.log('\n===== Employee Management System =====');
    console.log('1. Add Employee');
    console.log('2. List Employees');
    console.log('3. Remove Employee');
    console.log('4. Exit');
    rl.question('Choose an option: ', handleMenu);
}
function handleMenu(option) {
    switch(option.trim()) {
        case '1':
            addEmployee();
            break;
        case '2':
            listEmployees();
            break;
        case '3':
            removeEmployee();
            break;
        case '4':
            console.log('Exiting... Goodbye!');
            rl.close();
            break;
        default:
            console.log('Invalid option, try again.');
            showMenu();
    }
}
function addEmployee() {
    rl.question('Enter Employee ID: ', (id) => {
        rl.question('Enter Employee Name: ', (name) => {
            employees.push({ id: id.trim(), name: name.trim() });
            console.log(`Employee ${name.trim()} added successfully.`);
            showMenu();
        });
    });
}
function listEmployees() {
    console.log('\n--- Employee List ---');
    if(employees.length === 0) {
        console.log('No employees found.');
    } else {
        employees.forEach(emp => {
            console.log(`ID: ${emp.id}, Name: ${emp.name}`);
        });
    }
    showMenu();
}
function removeEmployee() {
    rl.question('Enter Employee ID to remove: ', (id) => {
        const index = employees.findIndex(emp => emp.id === id.trim());
        if(index !== -1) {
            const removed = employees.splice(index, 1);
            console.log(`Employee ${removed[0].name} removed successfully.`);
        } else {
            console.log('Employee not found.');
        }
        showMenu();
    });
}
showMenu();

