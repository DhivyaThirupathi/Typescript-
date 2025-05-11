
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dynamic Page with Background Video</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <style>
      
        .video-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            z-index: -1;
            background-color: black; 
        }

        .video-container video {
            width : 100vh;
            height: 100vh;
            object-fit: cover;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
        }

       
        .container-wrapper {
            perspective: 1000px; 
        }

        .container {
            max-width: 600px;
            background: rgba(0, 0, 0, 0.85);
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            animation: floatUpDown 3s infinite alternate ease-in-out; /* 2D Animation */
            transition: transform 0.5s ease-in-out;
            position: relative;
            transform-style: preserve-3d; 
        }

 
        @keyframes floatUpDown {
            from { transform: translateY(0); }
            to { transform: translateY(15px); }
        }

        .container:hover {
            transform: rotateY(20deg) rotateX(10deg);
            box-shadow: 0 15px 30px rgba(255, 255, 255, 0.5);
        }

        #myParagraph {
            display: none;
            font-size: 18px;
            padding: 10px;
            border-left: 5px solid #ffcc00;
            transition: all 0.5s ease;
        }

        #timeDifference {
            font-size: 16px;
            font-weight: bold;
            color: #ffcc00;
            margin-top: 10px;
        }
        
        #myLink, button {
            display: inline-block;
            margin: 10px;
            padding: 10px 20px;
            background-color: #ffcc00;
            color: black;
            text-decoration: none;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: transform 0.3s ease, background-color 0.3s;
        }

        #myLink:hover, button:hover {
            background-color: #ffaa00;
            transform: scale(1.1);
        }

        
        input {
            width: 90%;
            padding: 10px;
            margin: 10px 0;
            border: 2px solid white;
            border-radius: 5px;
            background: rgba(255, 255, 255, 0.1);
            color: white;
            transition: 0.3s;
        }

        input:focus {
            border-color: #ffcc00;
            box-shadow: 0 0 10px rgba(255, 204, 0, 0.7);
            outline: none;
        }
    </style>
</head>
<body>

   
    <div class="video-container">
        <video autoplay loop muted playsinline>
            <source src="https://ik.imagekit.io/mt9egd3uc/115425-704729723_small.mp4?updatedAt=1740753668206" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </div>
 
    <div class="container-wrapper">
    
        <div class="container">
            <a href="#" id="myLink">Click me to show paragraph</a>
            <p id="myParagraph">
                This paragraph appears dynamically and has a floating animation effect.
                Click it multiple times to change its style and track time differences.
            </p>
            <p id="timeDifference"></p>

            <form id="myForm">
                <label for="name">Name:</label>
                <input type="text" id="name" name="name" required>
                <button type="submit">Submit</button>
            </form>
        </div>
    </div>

    <script>
        $(document).ready(function() {
            let firstClickTime = null;
            const styles = [
                { color: 'yellow', fontSize: '20px', fontStyle: 'italic' },
                { color: 'red', fontSize: '22px', fontStyle: 'normal' },
                { color: 'lime', fontSize: '24px', fontStyle: 'bold' },
                { color: 'cyan', fontSize: '26px', fontStyle: 'oblique' },
                { color: 'magenta', fontSize: '28px', fontStyle: 'italic' }
            ];
            let currentStyleIndex = 0;

           
            $('#myLink').click(function(event) {
                event.preventDefault();
                $(this).fadeOut();
                $('#myParagraph').fadeIn(500);
            });

           
            $('#myParagraph').click(function() {
                const currentTime = new Date().getTime();

                $(this).css(styles[currentStyleIndex]);
                currentStyleIndex = (currentStyleIndex + 1) % styles.length;

                if (firstClickTime === null) {
                    firstClickTime = currentTime;
                } else {
                    const timeDifference = ((currentTime - firstClickTime) / 1000).toFixed(2);
                    $('#timeDifference').text(`Time between clicks: ${timeDifference} seconds`);
                    firstClickTime = currentTime;
                }
            });

            
            $('#myForm input').focus(function() {
                $(this).css({
                    'border-color': '#ffcc00',
                    'box-shadow': '0 0 10px rgba(255, 204, 0, 0.7)'
                });
            }).blur(function() {
                $(this).css({
                    'border-color': 'white',
                    'box-shadow': 'none' 
                });
            });

            $('.container').css("opacity", "1");
        });
    </script>

</body>
</html>
