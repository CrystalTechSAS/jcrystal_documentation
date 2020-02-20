SERVER.WEB 
SERVER.WEB.setBasePackage("torre.together");
SERVER.WEB.setEnableJSF(true);


SERVER.DEBUG.CORS = true;
		SERVER.DEBUG.ENTITY_CHECKS = true;
        		SERVER.DEBUG.LOG_EXCEPTIONS = true;


		SERVER.FIREBASE.setFirebaseDB("https://together-216714.firebaseio.com/");
		SERVER.FIREBASE.setFirebaseKey("together-216714-firebase-adminsdk-34rpg-9e49f055ce.json");