# TS Vision Motors - Salesforce Automation Project

## Project Overview

**What Next Vision Motors** is a comprehensive Salesforce automation project designed to streamline vehicle order processing with innovation and excellence. This project demonstrates advanced Salesforce development skills including custom objects, flows, triggers, and batch processing.

## 🎯 Project Goals

The main objectives of this project are to:

1. **Automate vehicle order processing** using Salesforce platform
2. **Assign orders to nearest dealers** based on customer location
3. **Prevent orders for out-of-stock vehicles** through validation logic
4. **Send automated email reminders** for test drives one day before scheduled date
5. **Manage inventory automatically** by reducing stock quantities when orders are confirmed

## 🛠️ Technologies Used

- **Salesforce Developer Edition**
- **Salesforce Flows** (Record-Triggered Flows)
- **Apex Classes and Triggers**
- **Batch Apex Classes**
- **Custom Objects and Fields**
- **Lightning App Builder**

## 📋 Project Structure

### Custom Objects Created

1. **Vehicle** (`Vehicle__c`)
   - Vehicle Name
   - Vehicle Model (Picklist: Sedan, SUV, EV, etc.)
   - Stock Quantity (Number)
   - Price (Currency)
   - Dealer (Lookup to Vehicle Dealer)
   - Status (Picklist: Available, Out of Stock, Discontinued)

2. **Vehicle Dealer** (`Vehicle_Dealer__c`)
   - Dealer Name
   - Location (Text)
   - Dealer Code (Auto Number: DC-0001)
   - Phone
   - Email

3. **Vehicle Customer** (`Vehicle_Customer__c`)
   - Customer Name
   - Email
   - Phone
   - Address
   - Preferred Vehicle Type (Picklist)

4. **Vehicle Order** (`Vehicle_Order__c`)
   - Order Number (Auto Number: O-0001)
   - Customer (Lookup to Vehicle Customer)
   - Vehicle (Lookup to Vehicle)
   - Order Date
   - Status (Picklist: Pending, Confirmed, Delivered, Cancelled)
   - Assigned Dealer (Lookup to Vehicle Dealer)

5. **Vehicle Test Drive** (`Vehicle_Test_Drive__c`)
   - Customer (Lookup to Vehicle Customer)
   - Vehicle (Lookup to Vehicle)
   - Test Drive Date
   - Status (Picklist: Scheduled, Completed, Cancelled)

6. **Vehicle Service Request** (`Vehicle_Service_Request__c`)
   - Customer (Lookup to Vehicle Customer)
   - Vehicle (Lookup to Vehicle)
   - Service Date
   - Issue Description
   - Status (Picklist: Requested, In Progress, Completed)

### Lightning App

- **App Name**: What Next Vision Motors
- **Included Objects**: All custom objects + Reports and Dashboards
- **User Profile**: System Administrator

## 🔄 Automation Components

### 1. Auto Assign Dealer Flow
**Type**: Record-Triggered Flow
**Trigger**: When Vehicle Order is created with Status = "Pending"

**Functionality**:
- Retrieves customer information
- Finds nearest dealer based on customer location
- Automatically assigns the dealer to the order

### 2. Test Drive Reminder Flow
**Type**: Record-Triggered Flow with Scheduled Path
**Trigger**: When Vehicle Test Drive status is updated to "Scheduled"

**Functionality**:
- Sends automated email reminder 1 day before test drive date
- Includes customer name and test drive ID
- Provides contact information for rescheduling

### 3. Apex Components

#### Vehicle Order Trigger Handler (`VehicleOrderTriggerHandler`)
- Manages order processing logic
- Reduces stock quantity when order status changes to "Confirmed"
- Prevents order creation for out-of-stock vehicles

#### Vehicle Order Trigger (`VehicleOrderTrigger`)
- Triggers on Vehicle Order insert/update operations
- Calls the trigger handler for processing

#### Batch Classes
- **Vehicle Order Batch**: Processes vehicle orders in batches
- **Vehicle Order Batch Scheduler**: Schedules batch jobs to run periodically
- Automatically updates order status to "Pending" for vehicles with zero stock

## 🚀 Setup Instructions

### Prerequisites
- Salesforce Developer Edition org
- System Administrator access

### Installation Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/yourusername/what-next-vision-motors.git
   cd what-next-vision-motors
   ```

2. **Deploy to Salesforce**
   - Use Salesforce CLI or deploy via Developer Console
   - Ensure all custom objects, fields, and Apex classes are deployed

3. **Configure Email Settings**
   - Update email templates with your organization's contact information
   - Configure email deliverability settings in Salesforce

4. **Test Data Setup**
   - Create sample Vehicle Dealer records
   - Add Vehicle records with appropriate stock quantities
   - Create Vehicle Customer records for testing

## 📊 Key Features Demonstration

### Inventory Management
- When an order status changes to "Confirmed", stock quantity automatically decreases
- System prevents order creation when stock quantity is 0
- Error message: "This vehicle is out of stock"

### Dealer Assignment
- Orders are automatically assigned to dealers based on customer location matching
- Uses exact location matching for dealer assignment

### Email Automation
- Test drive reminders sent exactly 24 hours before scheduled date
- Personalized emails with customer name and test drive details
- Professional email template with contact information

## 📁 Project Files Structure

```
salesforce-project/
├── objects/
│   ├── Vehicle__c/
│   ├── Vehicle_Dealer__c/
│   ├── Vehicle_Customer__c/
│   ├── Vehicle_Order__c/
│   ├── Vehicle_Test_Drive__c/
│   └── Vehicle_Service_Request__c/
├── flows/
│   ├── Auto_Assign_Dealer.flow
│   └── Test_Drive_Reminder.flow
├── classes/
│   ├── VehicleOrderTriggerHandler.cls
│   ├── VehicleOrderBatch.cls
│   └── VehicleOrderBatchScheduler.cls
├── triggers/
│   └── VehicleOrderTrigger.trigger
└── tabs/
    └── custom_tabs_metadata
```

## 🧪 Testing

### Manual Testing Steps

1. **Dealer Assignment Testing**:
   - Create a Vehicle Order with status "Pending"
   - Verify dealer is assigned based on customer location

2. **Inventory Management Testing**:
   - Confirm an order and check stock quantity reduction
   - Try creating order for zero-stock vehicle

3. **Email Reminder Testing**:
   - Schedule a test drive for tomorrow
   - Check email delivery within minutes

## 📈 Future Enhancements

- Integration with external mapping APIs for more sophisticated dealer assignment
- Advanced inventory management with reorder points
- Customer portal for self-service order tracking
- Mobile app integration
- Advanced reporting and analytics dashboards

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly in a Salesforce org
5. Submit a pull request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## 👤 Author

**Tushar Saxena**
- GitHub: [@ryl-tushar04](https://github.com/ryl-tushar04)
- LinkedIn: [@tushar-saxena0410](https://www.linkedin.com/in/tushar-saxena0410/)
## Acknowledgments

- Salesforce Developer Community
- Trailhead for comprehensive learning resources
- Topic Matters YouTube Channel for project guidance

---

**Note**: This project is designed for educational and demonstration purposes. Ensure proper testing and security reviews before deploying to production environments.
