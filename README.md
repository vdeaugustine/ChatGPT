<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<model type="com.apple.IDECoreDataModeler.DataModel" documentVersion="1.0" lastSavedToolsVersion="21513" systemVersion="22D68" minimumToolsVersion="Automatic" sourceLanguage="Swift" userDefinedModelVersionIdentifier="">
    <entity name="CalculatedPoints" representedClassName="CalculatedPoints" syncable="YES" codeGenerationType="class">
        <attribute name="amount" optional="YES" attributeType="Float" defaultValueString="0.0" usesScalarValueType="YES"/>
        <attribute name="playerId" optional="YES" attributeType="String"/>
        <attribute name="projectionType" optional="YES" attributeType="String"/>
        <attribute name="scoringName" optional="YES" attributeType="String"/>
        <relationship name="player" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="PlayerEntity" inverseName="calculatedPoints" inverseEntity="PlayerEntity"/>
        <relationship name="playerStats" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="PlayerStatsEntity" inverseName="calculatedPoints" inverseEntity="PlayerStatsEntity"/>
    </entity>
    <entity name="Draft" representedClassName="Draft" syncable="YES" codeGenerationType="class">
        <attribute name="creationDate" optional="YES" attributeType="Date" usesScalarValueType="NO"/>
        <attribute name="currentPick" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="currentProjection" optional="YES" attributeType="String"/>
        <attribute name="name" optional="YES" attributeType="String"/>
        <relationship name="draftedPlayers" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="DraftPlayer" inverseName="draft" inverseEntity="DraftPlayer"/>
        <relationship name="pool" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="PlayerPool" inverseName="draft" inverseEntity="PlayerPool"/>
        <relationship name="settings" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="DraftSettings" inverseName="drafts" inverseEntity="DraftSettings"/>
        <relationship name="teams" optional="YES" toMany="YES" deletionRule="Nullify" destinationEntity="DraftTeam" inverseName="draft" inverseEntity="DraftTeam"/>
    </entity>
    <entity name="DraftPlayer" representedClassName="DraftPlayer" syncable="YES" codeGenerationType="class">
        <attribute name="name" optional="YES" attributeType="String"/>
        <attribute name="pickNumber" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="playerId" optional="YES" attributeType="String"/>
        <attribute name="weightWhenDrafted" optional="YES" attributeType="Float" defaultValueString="0.0" usesScalarValueType="YES"/>
        <relationship name="draft" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="Draft" inverseName="draftedPlayers" inverseEntity="Draft"/>
        <relationship name="player" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="PlayerEntity" inverseName="draftPlayer" inverseEntity="PlayerEntity"/>
        <relationship name="playerStat" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="PlayerStatsEntity" inverseName="draftPlayer" inverseEntity="PlayerStatsEntity"/>
        <relationship name="team" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="DraftTeam" inverseName="players" inverseEntity="DraftTeam"/>
    </entity>
    <entity name="DraftSettings" representedClassName="DraftSettings" syncable="YES" codeGenerationType="class">
        <attribute name="isSnakeDraft" optional="YES" attributeType="Boolean" usesScalarValueType="YES"/>
        <attribute name="numberOfRounds" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="numberOfTeams" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="playersPerTeam" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <relationship name="drafts" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="Draft" inverseName="settings" inverseEntity="Draft"/>
        <relationship name="rosterRequirements" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="RosterRequirements" inverseName="draftSettings" inverseEntity="RosterRequirements"/>
        <relationship name="scoringSystems" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="ScoringSettings" inverseName="draftSettings" inverseEntity="ScoringSettings"/>
    </entity>
    <entity name="DraftTeam" representedClassName="DraftTeam" syncable="YES" codeGenerationType="class">
        <attribute name="draftPosition" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="name" optional="YES" attributeType="String"/>
        <relationship name="draft" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="Draft" inverseName="teams" inverseEntity="Draft"/>
        <relationship name="players" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="DraftPlayer" inverseName="team" inverseEntity="DraftPlayer"/>
    </entity>
    <entity name="PlayerEntity" representedClassName="PlayerEntity" syncable="YES" codeGenerationType="class">
        <attribute name="id" attributeType="String"/>
        <attribute name="isStar" optional="YES" attributeType="Boolean" usesScalarValueType="YES"/>
        <attribute name="name" optional="YES" attributeType="String"/>
        <attribute name="position" optional="YES" attributeType="String"/>
        <attribute name="teamFull" optional="YES" attributeType="String"/>
        <attribute name="teamShort" optional="YES" attributeType="String"/>
        <relationship name="calculatedPoints" optional="YES" toMany="YES" deletionRule="Nullify" destinationEntity="CalculatedPoints" inverseName="player" inverseEntity="CalculatedPoints"/>
        <relationship name="draftPlayer" optional="YES" toMany="YES" deletionRule="Nullify" destinationEntity="DraftPlayer" inverseName="player" inverseEntity="DraftPlayer"/>
        <relationship name="stats" optional="YES" toMany="YES" deletionRule="Cascade" destinationEntity="PlayerStatsEntity" inverseName="player" inverseEntity="PlayerStatsEntity"/>
    </entity>
    <entity name="PlayerPool" representedClassName="PlayerPool" syncable="YES" codeGenerationType="class">
        <relationship name="availablePlayers" optional="YES" toMany="YES" deletionRule="Nullify" destinationEntity="PlayerStatsEntity" inverseName="pool" inverseEntity="PlayerStatsEntity"/>
        <relationship name="draft" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="Draft" inverseName="pool" inverseEntity="Draft"/>
    </entity>
    <entity name="PlayerStatsEntity" representedClassName="PlayerStatsEntity" syncable="YES" codeGenerationType="class">
        <attribute name="ab" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="adp" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="avg" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="babip" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="baseRunning" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="bb" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="bbPercentage" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="bbPerK" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="cs" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="def" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="g" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="gdp" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="gdpRuns" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="h" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="hbp" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="hr" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="ibb" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="iso" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="kPercentage" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="League" optional="YES" attributeType="String"/>
        <attribute name="minpos" optional="YES" attributeType="String"/>
        <attribute name="obp" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="offense" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="oneB" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="ops" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="pa" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="playerids" optional="YES" attributeType="String"/>
        <attribute name="playerName" optional="YES" attributeType="String"/>
        <attribute name="Pos" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="projectionType" optional="YES" attributeType="String"/>
        <attribute name="r" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="rbi" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="sb" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="sf" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="sh" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="slg" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="so" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="spd" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="tb" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="teamid" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="threeB" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="twoB" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="ubr" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="uzr" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="war" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="wBsR" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="wOBA" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="wRAA" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="wRC" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="wRCPlus" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <relationship name="calculatedPoints" optional="YES" toMany="YES" deletionRule="Nullify" destinationEntity="CalculatedPoints" inverseName="playerStats" inverseEntity="CalculatedPoints"/>
        <relationship name="draftPlayer" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="DraftPlayer" inverseName="playerStat" inverseEntity="DraftPlayer"/>
        <relationship name="player" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="PlayerEntity" inverseName="stats" inverseEntity="PlayerEntity"/>
        <relationship name="pool" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="PlayerPool" inverseName="availablePlayers" inverseEntity="PlayerPool"/>
    </entity>
    <entity name="RosterRequirements" representedClassName="RosterRequirements" syncable="YES" codeGenerationType="class">
        <attribute name="min1B" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="min2B" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="min3B" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="minOF" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="minRP" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="minSP" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="minSS" optional="YES" attributeType="Integer 16" defaultValueString="0" usesScalarValueType="YES"/>
        <relationship name="draftSettings" optional="YES" maxCount="1" deletionRule="Nullify" destinationEntity="DraftSettings" inverseName="rosterRequirements" inverseEntity="DraftSettings"/>
    </entity>
    <entity name="ScoringSettings" representedClassName="ScoringSettings" syncable="YES" codeGenerationType="class">
        <attribute name="batterK" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="bb" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="cs" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="er" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="hitsAllowed" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="ip" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="key" optional="YES" attributeType="String"/>
        <attribute name="losses" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="name" attributeType="String"/>
        <attribute name="pitcherK" optional="YES" attributeType="Float" defaultValueString="0.0" usesScalarValueType="YES"/>
        <attribute name="qs" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="r" optional="YES" attributeType="Float" defaultValueString="0.0" usesScalarValueType="YES"/>
        <attribute name="rbi" optional="YES" attributeType="Float" defaultValueString="0.0" usesScalarValueType="YES"/>
        <attribute name="saves" optional="YES" attributeType="Float" defaultValueString="0.0" usesScalarValueType="YES"/>
        <attribute name="sb" optional="YES" attributeType="Float" defaultValueString="0.0" usesScalarValueType="YES"/>
        <attribute name="tb" optional="YES" attributeType="Float" defaultValueString="0" usesScalarValueType="YES"/>
        <attribute name="walksAllowed" optional="YES" attributeType="Float" defaultValueString="0.0" usesScalarValueType="YES"/>
        <attribute name="wins" optional="YES" attributeType="Float" defaultValueString="0.0" usesScalarValueType="YES"/>
        <relationship name="draftSettings" optional="YES" toMany="YES" deletionRule="Nullify" destinationEntity="DraftSettings" inverseName="scoringSystems" inverseEntity="DraftSettings"/>
        <uniquenessConstraints>
            <uniquenessConstraint>
                <constraint value="name"/>
            </uniquenessConstraint>
        </uniquenessConstraints>
    </entity>
</model>
