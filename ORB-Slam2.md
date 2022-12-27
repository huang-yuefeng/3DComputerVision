```graphTD

			Start((Start)) --> NotInit
			MonoInit --> Init
			MonoInitWithMap --> Init
			NotInit((Not Initialized)) --> NoMap((No Map))
			NoMap --> MonoInit(Monocular Initialization)
			NotInit --> Map
			Map((Map)) --> MonoInitWithMap(Monocular Initialization With Map)
			Init --> NotOnlyTrack((Not Only Tracking))
			Init((Initialized)) --> OnlyTrack
			OnlyTrack((Only Tracking)) --> Lost
			OnlyTrack --> NotLostOT((Not Lost))
			Lost((Lost)) --> Relo(Relocalization)
			NotOnlyTrack --> NotLost((Not Lost))
			NotOnlyTrack --> Lost
			NotLost --> NotHaveSpeed((Not Have Speed))
			NotLost --> HaveSpeed((Have Speed))
			HaveSpeed --> TrackWithMotion(Track With Motion)
			
			NotLostOT --> EnoughMapPoint((Enough Map Points))
			EnoughMapPoint --> NotLost
			NotLostOT --> NotEnoughMapPoint((Not Enough Map Points))
			NotEnoughMapPoint --> Relo	
			NotEnoughMapPoint --> ReloNotOK((Relocalized Not OK))
			ReloNotOK --> HaveSpeed		
			
			
			TrackWithMotion --> NotOK((Track Not OK))
			TrackWithMotion --> OK((Track OK))
			NotOK --> TrackWithReferenceKeyFrame(Track With Reference Key Frame)
			NotHaveSpeed --> TrackWithReferenceKeyFrame
			TrackWithReferenceKeyFrame --> OK
			Relo --> OK
			

			OK --> OTrack((Only Tracking))
			OTrack --> TrackLocalMap(Track Local Map)
			OK --> EMapPoint((Enough Map Points))
			EMapPoint --> TrackLocalMap
```
