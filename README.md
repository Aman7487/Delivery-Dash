Unity 2D Delivery Dash
A 2D delivery-driving game built with Unity and C#. The player drives a car, picks up packages, delivers them to customers, and can collect speed boosts while navigating the game world.
Features
- Car movement: Drive forward and backward using W and S.
- Steering: Rotate the car using A and D.
- Speed boost: Collect a boost object to increase the car's speed.
- Collision response: Restore regular speed when colliding with an object tagged WorldCollision.
- Package pickup: Pick up a package when the car overlaps an object tagged Package.
- Delivery system: Deliver the package by reaching an object tagged Customer.
- Visual feedback: Play a Particle System effect while carrying a package and show a boost indicator.
- Object management: Remove collected objects and delivered customers from the scene.
Built With
- Unity
- C#
- Unity Input System
- TextMeshPro
- Unity 2D Physics and colliders
Project Scripts
Driver.cs
Responsible for driving and boost mechanics.
- Reads keyboard input using Keyboard.current.
- Uses W and S for forward/backward movement.
- Uses A and D for steering.
- Uses Time.deltaTime to scale movement and rotation by elapsed frame time.
- Collects objects tagged Boost.
- Increases currentSpeed to boostSpeed and displays the boost text.
- Resets speed to regularSpeed after a collision with an object tagged WorldCollision.
Delivery.cs
Responsible for package pickup and delivery logic.
- Uses the Boolean hasPackage to track whether the car is carrying a package.
- Picks up an object tagged Package only when the car is not already carrying one.
- Plays a Particle System effect on pickup.
- Schedules the package object for destruction after delay seconds.
- Delivers the package when the car enters an object tagged Customer while carrying a package.
- Resets hasPackage and stops the Particle System after delivery.
Current behavior: The supplied Delivery.cs destroys the customer GameObject after a successful delivery. Adjust this if customers should accept multiple deliveries.

Controls
Key	Action
W	Move forward
S	Move backward
A	Steer in the positive Z-rotation direction
D	Steer in the negative Z-rotation direction


The visible turning direction depends on the car sprite's initial orientation.
Unity Scene Setup
For the supplied scripts to work as intended:
1. Attach Driver.cs to the car GameObject.
2. Attach Delivery.cs to the appropriate car GameObject.
3. Configure 2D colliders for the car, packages, customers, boosts, and world objects.
4. Set the relevant GameObject tags exactly as follows:
   - Package
   - Customer
   - Boost
   - WorldCollision
5. Configure trigger colliders for objects detected by OnTriggerEnter2D.
6. Configure colliders and the required Rigidbody2D setup for trigger and collision callbacks.
7. Assign the boostText TextMeshPro reference in the Inspector.
8. Ensure a Particle System component is available on the same GameObject as Delivery.cs.
9. Ensure the Unity Input System package is enabled and a keyboard is available.
10. Adjust speed and delay values in the Inspector to tune gameplay.
How the Main Logic Works
Package and delivery flow
1. The car starts with hasPackage = false.
2. Entering a Package trigger while empty sets hasPackage = true.
3. The pickup effect plays and the package object is scheduled for destruction.
4. Entering a Customer trigger while carrying a package completes the delivery.
5. The script sets hasPackage = false, stops the effect, and destroys the customer object.
Speed boost flow
1. The car enters a trigger tagged Boost.
2. currentSpeed changes to boostSpeed.
3. The boost text becomes visible and the boost object is destroyed.
4. A collision with an object tagged WorldCollision restores regularSpeed and hides the boost text.
Technical Concepts Practised
- Unity MonoBehaviour lifecycle methods: Start() and Update()
- C# variables, Boolean state, conditionals, and logical operators
- Unity Transform movement and rotation
- Frame-time scaling with Time.deltaTime
- Unity Input System keyboard input
- OnTriggerEnter2D and OnCollisionEnter2D
- GameObject tags and CompareTag()
- Component access with GetComponent<T>()
- SerializeField and Inspector configuration
- Particle System effects
- TextMeshPro UI
- Delayed and immediate object destruction
Possible Improvements
- Add a timed boost duration if the boost should expire automatically.
- Validate or cache component references to avoid NullReferenceException.
- Use Input Actions for configurable controls and additional input devices.
- Add a delivery counter, score, sound effects, or completion UI.
- Separate input, movement, UI, and delivery management as the project grows.
- Consider Rigidbody2D-based movement if physics-driven interactions are required.
- Add clear handling for repeated customer deliveries if customers should remain in the scene.
Learning Outcomes
This project demonstrates practical experience with Unity's component-based workflow, C# scripting, player input, 2D trigger and collision events, simple gameplay state management, UI feedback, and GameObject lifecycle management.
Project Status
A learning project based on the provided Driver.cs and Delivery.cs scripts. Features described here are limited to the supplied code and project lesson list; confirm any additional tutorial features against the actual Unity scene before describing them as implemented.
