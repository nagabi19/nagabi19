from tinydb import TinyDB, Query

# Initialize TinyDB and create a database file
db = TinyDB('home_automation_db.json')

# Define a table for devices
devices_table = db.table('devices')

# Define a table for actions
actions_table = db.table('actions')

# Example: Inserting a device into the devices table
devices_table.insert({'name': 'Light Bulb', 'type': 'light', 'status': 'off'})

# Example: Inserting an action into the actions table
actions_table.insert({'device_id': 1, 'action': 'turn_on', 'timestamp': '2023-11-13 12:00:00'})

# Example: Querying the devices table to get the status of a specific device
Device = Query()
result = devices_table.search(Device.name == 'Light Bulb')
if result:
    device_status = result[0]['status']
    print(f"The status of the Light Bulb is {device_status}")
else:
    print("Device not found")

# Example: Updating the status of a device
devices_table.update({'status': 'on'}, Device.name == 'Light Bulb')

# Example: Querying the actions table to get a history of actions for a device
actions_history = actions_table.search(Device.name == 'Light Bulb')
print("Actions history for the Light Bulb:")
for action in actions_history:
    print(f"Action: {action['action']}, Timestamp: {action['timestamp']}")






