//Island related Contracts
//CONTENT:
//Fly over the island

CONTRACT_TYPE
{
	//Stuff to define the relation of the contract
	name = VisitIsland
    	title = Fly over the island
    	group = Island				
	agent = Kerbal Aircraft Builders
   	//Messages and descriptions
    	description = Fly over to the island and check the situation
    	synopsis = We want to know whats going on over there.
	completedMessage = Mission Accomplished!
	//All the data for mission control
    	minExpiry = 1.0
    	maxExpiry = 7.0
	deadline = 500
	cancellable = true
	declinable = true
    	autoAccept = false
   	targetBody = Kerbin
   	maxCompletions = 1
   	maxSimultaneous = 1
	//rewards and penalties
 	rewardScience = 5.0
  	rewardReputation = 16.0
  	rewardFunds = 7000.0
 	failureReputation = 16.0
  	failureFunds = 7000.0
  	advanceFunds = 4000.0
	weight = 10.0
	//Here starts the contract, each PARAMETER in this Tab is a main parameter
	PARAMETER
	{
		//This defines the vessel as Plane8 for the rest of the contract and will be refered to in the next main PARAMETERS
		name = VesselParameterGroup
		type = VesselParameterGroup
		define = Plane8
		//This will also show in every main PARAMETER and forces the player to complete them all in sequence
		completeInSequence = true
		//This one is a child to the first parameter
		PARAMETER
		{
			//This just makes clear, that it has to be a manned vessel
			name = HasCrew
			type = HasCrew
			minCrew = 1
		}
	}
	
	PARAMETER
	{
		//The stuff explained above
		name = VesselParameterGroup2
		type = VesselParameterGroup
		vessel = Plane8
		completeInSequence = true
	
		PARAMETER
		{
			//Thats the Waypoint, wich will be created at the end of this contract
			name = WP0        
			type = All
        
			title = Flyby
		}
		//This is a sibling to the PARAMETERS above and below, they all have to be completed for the main PARAMETER 
		PARAMETER
        	{
        		//This wants the vessel to be FLYING at the waipoint
        		name = ReachState    
			type = ReachState 
			situation = FLYING       
		}

    

		PARAMETER
		{
			//And this defines the allowed max distance to the waypoint to be concidered "visited"
			name = VisitWaypoint
            		type = VisitWaypoint

            		index = 0
            
			distance = 1000	
		}
	}
	//Vessel definition again
	PARAMETER
	{
		name = VesselParameterGroup2
		type = VesselParameterGroup
		vessel = Plane8
		completeInSequence = true
		//This one wants the vessel to be LANDED at a specific biome
		PARAMETER
		{
			name = land
			type = ReachState
			
			situation = LANDED
			biome = Runway
		}
		//And this one also wants the vessel to remain LANDED for 10seconds
		PARAMETER
		{
			name = Duration
			type = Duration
			duration = 10s
			preWaitText = Land and wait
			waitingText = A bit longer
			completionText = DONE!
		}
	}
	//The final main PARAMETER makes sure the vessel is stil intact
	PARAMETER
	{
   		name = VesselNotDestroyed
    		type = VesselNotDestroyed
		completeInSequence = true
	}
	//And like mentioned above this creates a waypoint
	BEHAVIOUR
    
	{
        
		name = WaypointGenerator
        
		type = WaypointGenerator

 
       		//namly this waypoint at those specific koordinates
		WAYPOINT       
		{
            
			name = Island          
			icon = marker
			altitude = 2000.0
			latitude = -1.6
            		longitude = -71.85
		}
	}
	
   
}
