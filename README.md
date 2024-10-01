


# MapMitra: Navigate Effortlessly

**MapMitra** is a navigation and real-time transportation tracking system built specifically for campus environments. It provides intuitive, landmark-based directions and real-time e-rickshaw tracking, offering a seamless and efficient experience for students, visitors, and e-rickshaw users.

## Table of Contents
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Landmark-Based Navigation**: Provides clear, recognizable directions using familiar campus landmarks.
- **Real-Time E-Rickshaw Tracking**: Allows users to track nearby e-rickshaws and view estimated arrival times.
- **Ride Hailing**: Users can hail an e-rickshaw directly from the app, reducing wait times.
- **Personalized Recommendations**: Suggests campus-relevant places like eateries and services based on user preferences.
- **Admin Interface**: Manage routes, road closures, and e-rickshaw registrations.

## Technologies Used

- **Next.js**: Server-side rendering framework for building the frontend and backend.
- **MongoDB**: Database for managing user data, tracking information, and campus landmarks.
- **Redis**: Used for caching data to improve performance.
- **Socket.io**: Enables real-time communication for live e-rickshaw tracking and notifications.
- **OpenStreetMap**: Provides detailed maps and geographic data.

## Installation

To install and run this project locally, follow these steps:

1. Clone the repository:

    ```bash
    git clone https://github.com/your-username/MapMitra.git
    ```

2. Navigate to the project directory:

    ```bash
    cd MapMitra
    ```

3. Install the dependencies:

    ```bash
    npm install
    ```

4. Create a `.env` file with the following environment variables:

    ```bash
    DATABASE_URL=your_mongodb_url
    REDIS_URL=your_redis_url
    SOCKET_PORT=your_socket_port
    ```

5. Start the development server:

    ```bash
    npm run dev
    ```

6. Open your browser and visit `http://localhost:3000`.

## Usage

- **For Students and Visitors**: Use the app to navigate the campus with ease by following directions based on campus landmarks. Track and hail e-rickshaws in real-time for fast and efficient transport.
- **For E-Rickshaw Drivers**: Use the driver interface to accept ride requests, view user locations, and manage availability.
- **For Administrators**: Manage the campus map, add or update routes, register new e-rickshaws, and monitor road closures.

## Contributing

We welcome contributions to improve MapMitra! To contribute:

1. Fork the repository.
2. Create a new branch for your feature (`git checkout -b feature-name`).
3. Commit your changes (`git commit -m 'Add new feature'`).
4. Push to your branch (`git push origin feature-name`).
5. Create a pull request.

Please ensure your code follows the project's coding standards and is well-documented.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

---

