# RelationalChirper SQL Code


	CREATE SCHEMA relational_chirper;
    USE relational_chirper;

    CREATE TABLE clients (
    id INT AUTO_INCREMENT,
    handle VARCHAR(50),
    email VARCHAR(70),
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY(id) 
	);
    
    CREATE TABLE tweets (
		id INT AUTO_INCREMENT,
        clients_id INT,
        body VARCHAR(150),
        location VARCHAR(70),
        created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
        PRIMARY KEY (id),
        FOREIGN KEY (clients_id) REFERENCES clients (id)
        );
        
	INSERT INTO clients (handle, email) VALUES
    ('qbnate08', 'Nate Mills'),
    ('rouxG', 'Roux The Golden'),
    ('bennyH', 'Benson The Cat'),
    ('leoK', 'Leo The Dog'),
    ('dreamcatcher', 'Big Bird the Bird');
    
     INSERT INTO tweets (body, location) VALUES
    ('Did you hear they arrested the devil? Yeah they got him on possession', 'Tampa,FL'),
    ('My IQ test results came back. They were negative', 'St.Louis, MO'),
    ('What do you get when you cross a polar bear with a seal? A polar bear','Lyndhurst,OH'),
    ('Why was six afraid of seven? Because seven eight nine', 'New York, NY'),
    ('Can we stop with all of the corny Jokes','Detroit, MI');
    
    INSERT INTO clients (handle) VALUE 
    ('King Kong');
    
    ALTER TABLE tweets MODIFY clients_id INT NOT NULL;
    
    UPDATE tweets SET clients_id = 1 WHERE id = 1;
    UPDATE tweets SET clients_id = 2 WHERE id = 2;
    UPDATE tweets SET clients_id = 3 WHERE id = 3;
    UPDATE tweets SET clients_id = 4 WHERE id = 4;
    UPDATE tweets SET clients_id = 5 WHERE id = 5;
    
    SELECT * FROM clients;
    
    SELECT * FROM tweets;
    
    
    
    SELECT
    clients.id,
    clients.handle,
    clients.email,
    clients.created_at,
    tweets.body AS Tweet,
    tweets.location as Location
	FROM tweets
    JOIN clients ON clients.id = tweets.clients_id;
    
    CREATE TABLE mentions (
    id INT AUTO_INCREMENT,
    tweets_id INT,
    clients_id INT,
    mentions VARCHAR(80),
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
	PRIMARY KEY (id),
    FOREIGN KEY (tweets_id) REFERENCES tweets (id),
    FOREIGN KEY (clients_id) REFERENCES clients (id)
    );
    
    UPDATE tweets SET body ='Hey @leoK Did you hear they arrested the devil? Yeah they got him on possession' WHERE id = 1;
    UPDATE tweets SET body = 'Hey @qbnate08, My IQ test results came back. They were negative' WHERE id = 2;
    UPDATE tweets SET body = 'Hey @dreamcatcher, What do you get when you cross a polar bear with a seal? A polar bear' WHERE id = 3;
    
    
    INSERT INTO mentions (tweets_id, clients_id) VALUE (1,4);
    INSERT INTO mentions (tweets_id, clients_id) VALUE (2,1);
    INSERT INTO mentions (tweets_id, clients_id) VALUE (3,5);
    
    SELECT
    clients.id,
    clients.handle,
    clients.email,
    tweets.body AS Tweet,
    tweets.location AS Location,
    mentions.tweets_id AS MentionedBy,
    mentions.clients_id AS Mentioned
    FROM tweets 
    JOIN clients ON clients.id = tweets.clients_id
    JOIN mentions ON mentions.tweets_id = tweets.id
    JOIN clients mu ON mu.id = mentions.clients_id;
    
    
    
    
    
