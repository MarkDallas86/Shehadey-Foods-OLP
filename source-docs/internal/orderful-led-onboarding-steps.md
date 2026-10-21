Orderful Led Projects Onboarding Steps: 
Work flow: 

1. Orderful notifies Concurrent of new Client > Slack
2. Orderful schedules kick off call
3. [Optional] For projects involving a connector. Concurrent emails the client the Connector questionnaire with instructions (which tabs are relevant, etc) to the client and asks them to have it filled out before the Kick off call.  
4. Requirements from Orderful before Kick off call 
    1. Provide Concurrent Orderful Org Access
    2. Provide KT with
        1. Kick off deck
        2. Client info, contacts
        3. Confirm Connector project or no
        4. Trans types (850, 940, etc.)
        5. Go Live Date
5. Requirements from Concurrent before Kick off call 
    1. Do we support the connector requested? 
    2. Does the Go Live date requested by the client fall within our standard timeline to support it? 
    3. Any other concerns to escalate internally before the Kick off call? 
    4. Run the Claude Start Project (Bentley preforms this) 
        1. Asana 
            1. Concurrent PM to update the Asana Timeline 
            2. [Optional for time sensitive clients] Use the timeline from Asana to present to the client on the Kickoff call. 
        2. Jira 
6. Kick off call
    1. Concurrent PM reviews: 
        1. Timeline 
        2. Confirms TPs, Trans types, connector info
        3. Clearly calls out dependencies, and the affects on timeline of delays from the client and the TPs. Give examples! 
    2. Confirm that Orderful adds all client users to Orderful Org. 
    3. [Optional] For projects 1) involving a connector or 2) projects that need to be closely monitored or are complex - 
        1. Concurrent PM should Schedule a weekly touch base meeting with the client and the Concurrent technical resource and the Client's technical resource and or client's PM 
7. Client submits trade request 
8. Orderful Onboarding support (i.e. Bender / Onboarding agent in Orderful MTS Slack channel) follows up with the client to confirm if TP has submitted trade requests. Concurrent may take the lead on this as well. 
9. TP responds with all trade request info
    1. If the TP is already in Orderful, all details will be present there, confirmations may not be needed. 
10. The Trade Request in some cases (if outreach CB is set to yes) will generate an automated email 
11. Orderful confirms connectivity with TP for testing. 
    1. Orderful Onboarding support (i.e. Mykee or Priya) will need to follow up with the trading partner via email to confirm connectivity. This usually involves sending and receiving an initial acknowledgement or a transaction like an EDI 850. 
    2. Once connectivity is established with the TP, this is the hand off from responsibility between Orderful and Concurrent. 
    3. !!! [Needs definition] How does the Orderful Onboarding person notifiy the Concurrent OBM to begin work on Testing? 
        1. Slack channel? 
        2. Email thread with client and TP? 
12. The Concurrent PM / Onboarding Manager confirms testing plan with TP by following up in the email thread that Orderful began above. Confirms: 
    1. testing portal vs over testing over email
    2. # of test 850s required to be processed by the TP, etc.)
    3. Concurrent PM ensures Onboarding Managers (OBMs) follow the testing plan as laid out by the TP. 
13. Concurrent OBM confirms relationships in Orderful Org., if any are missing, Orderful sets them up. 
14. Concurrent OBM pushes test 850s to client SOR.
15. Concurrent OBM notifies client of the results / status of pushing 850s to their SOR and of next steps. 
16. Concurrent tests other Inbound to Orderful transactions (800 series - 860, etc)
17. Client notifies Concurrent when they are ready to test Outbound to Orderful transactions (855, 856, 810). 
18. Concurrent pushes Outbound transactions to TP and completes TP testing requirements. 
19. Concurrent provides TP feedback to the client as needed to complete test cycle. 
20. Concurrent PM / OBM notifies client to begin UAT
21. Once TP testing requirements are complete and client UAT is complete, Concurrent PM confirms with Orderful if all cutover steps are complete. 
22. Relationships in Orderful 
    1. Skip TP testing step
    2. Move each relationship to Live
23. Confirm go live with all parties involved. 
24. Monitor first live transactions (if available). 

