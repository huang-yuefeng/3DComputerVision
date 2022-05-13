graph TB
    %%subgraph Thread1
    %%    performLoopClosure
    %% end



    %%subgraph Thread2
    %%    visualizeMapThread
    %%end

    subgraph MainThread
        direction TB
        subgraph transformAssociateToMap
            direction TB
            transformIncre --> transformTotransformTobeMapped
        end
        transformBefMapped --transform to-->transformIncre
        transformSum --transform to--> transformIncre
        transformAftMapped ---> transformTotransformTobeMapped
        transformTotransformTobeMapped ---> transformTobeMapped

        subgraph extractSurroundingKeyFrames
            direction TB
        end
        subgraph downsampleCurrentScan
            direction TB
            downSizeFilterScancontext ---> laserCloudRawDS ---> downsampleCurrentScanfinish
            downSizeFilterCorner ---> laserCloudCornerLastDS ---> downsampleCurrentScanfinish
            downSizeFilterSurf ---> laserCloudSurfLastDS
            downSizeFilterOutlier ---> laserCloudOutlierLastDS
            downSizeFilterSurf ---> laserCloudSurfTotalLastDS ---> downsampleCurrentScanfinish
            laserCloudOutlierLastDS ---> laserCloudSurfTotalLast 
            laserCloudSurfLastDS ---> laserCloudSurfTotalLast
            laserCloudSurfTotalLast ---> downSizeFilterSurf
        end
        laserCloudRawHandler ---> laserCloudRaw ---> downSizeFilterScancontext
        laserCloudCornerLastHandler ---> laserCloudCornerLast ---> downSizeFilterCorner
        laserCloudOutlierLastHandler ---> laserCloudOutlierLast ---> downSizeFilterOutlier
        laserCloudSurfLastHandler ---> laserCloudSurfLast ---> downSizeFilterSurf

        subgraph scan2MapOptimization
            direction TB
            cornerOptimization --> surfOptimization --> LMOptimization --> transformUpdate
            transformUpdate -- time interplation --> IMUPitch&Roll --> updatetransformTobeMapped --> updatetransformAftMapped --> updatetransformBefMapped
        end
        downsampleCurrentScanfinish ---> cornerOptimization
        updatetransformTobeMapped --weighed IMUPitch&Roll--> transformTobeMapped
        updatetransformAftMapped --transformTobeMapped-->transformAftMapped
        updatetransformBefMapped --transformSum--> transformBefMapped

        subgraph saveKeyFramesAndFactor
            direction TB
            updateCurrentPos --> etermineKeyFrameByDistance --> updatePreviousPos --> isam
            isam --> addFirstPoint --> calculateEstimate
            isam --> addEdge --> calculateEstimate
            addFirstPoint --transformTobeMapped--> transformLast
            calculateEstimate --> allEstimate --> latestEstimate --> storeKeyFrames --> makeAndSaveScancontextAndKeys
        end
        transformTobeMapped --> transformLast
        transformAftMapped --> currentRobotPosPoint
        currentRobotPosPoint --> DetermineKeyFrameByDistance
        previousRobotPosPoint --> DetermineKeyFrameByDistance
        updatePreviousPos --currentRobotPosPoint--> previousRobotPosPoint
        updatetransformBefMapped --> updateCurrentPos
        updateCurrentPos --transformAftMapped--> currentRobotPosPoint
        currentRobotPosPoint --> previousRobotPosPoint
        latestEstimate --> cloudKeyPoses3D
        latestEstimate --> cloudKeyPoses6D
        latestEstimate --> transformAftMapped
        storeKeyFrames --laserCloudCornerLastDS--> cornerCloudKeyFrames
        laserCloudCornerLastDS --> cornerCloudKeyFrames
        storeKeyFrames --thisSurfKeyFrame--> surfCloudKeyFrames
        thisSurfKeyFrame--> surfCloudKeyFrames
        storeKeyFrames --thisOutlierKeyFrame--> outlierCloudKeyFrames
        thisOutlierKeyFrame--> outlierCloudKeyFrames
        laserCloudSurfLastDS --> makeAndSaveScancontextAndKeys
        laserCloudRawDS --> makeAndSaveScancontextAndKeys

        subgraph correctPoses
            direction TB
            correctAllPoses
        end
        correctAllPoses --allEstimate--> cloudKeyPoses3D
        allEstimate--> cloudKeyPoses3D
        correctAllPoses --allEstimate--> cloudKeyPoses6D
        allEstimate--> cloudKeyPoses6D
        makeAndSaveScancontextAndKeys --> correctAllPoses

        subgraph publishTF
            direction TB
            odomAftMapped --> pose
            odomAftMapped --> twist
            odomAftMapped --> publish
        end
        correctAllPoses --> odomAftMapped
        transformAftMapped --> pose
        transformBefMapped --> twist

        subgraph publishKeyPosesAndFrames
            direction TB
            pubKeyPoses
            pubRecentKeyFrames
            pubRegisteredCloud
        end
        cloudKeyPoses3D --> pubKeyPoses
        laserCloudSurfFromMapDS --> pubRecentKeyFrames
        laserCloudCornerLastDS --> pubRegisteredCloud
        laserCloudSurfTotalLast --> pubRegisteredCloud
        transformTobeMapped --> pubRegisteredCloud
        subgraph clearCloud
            direction TB
        as7
        end

        laserOdometryHandler --subscribe message--> transformSum           
    end

    %%OtherNodes --subscribe message--> laserCloudRaw
    %%OtherNodes --subscribe message--> laserCloudOutlierLast
    %%OtherNodes --subscribe message--> laserCloudCornerLast
    %%OtherNodes --subscribe message--> laserCloudSurfLast
    %%OtherNodes --subscribe message--> imuTime/Roll/Pitch
    
    transformAftMapped
    transformTobeMapped
