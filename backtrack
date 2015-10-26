backtrackingNodes = 0 # profiling variable to track number of state-space tree nodes
def main():
    #changeAmt = int(input("Enter the change amount: "))
    changeAmt = 20
    coinTypes = input("Enter the coin types separated by spaces: ")
    coinTypes = coinTypes.split(" ")
    for index in range(len(coinTypes)):
        coinTypes[index] = int(coinTypes[index])
    print ("Change Amount: " ,changeAmt, " Coin types : " , coinTypes)
    fewestCoins, numberOfEachCoinType = solveCoinChange(changeAmt, coinTypes)
    print ("Fewest number of coins",fewestCoins)
    print ("The number of each type of coin in the solution is:")
    for index in range(len(coinTypes)):
        print ("number of %s-cent coins is %s"%(str(coinTypes[index]), str(numberOfEachCoinType[index])))
    return

def solveCoinChange(changeAmt, coinTypes):
    
    def backtrack(changeAmt, numberOfEachCoinType, numberOfCoinsSoFar, solutionFound, bestFewestCoins, bestNumberOfEachCoinType):
        global backtrackingNodes
        backtrackingNodes += 1

        for index in range(len(coinTypes)):
            smallerChangeAmt = changeAmt - coinTypes[index]
            if promising(smallerChangeAmt, numberOfCoinsSoFar+1, solutionFound, bestFewestCoins):
                if smallerChangeAmt == 0: # a solution is found
                    if (not solutionFound) or numberOfCoinsSoFar + 1 < bestFewestCoins: # check if its best
                        bestFewestCoins = numberOfCoinsSoFar+1
                        bestNumberOfEachCoinType = [] + numberOfEachCoinType
                        bestNumberOfEachCoinType[index] += 1
                        solutionFound = True
                else:
                    # call child with updated state information
                    smallerChangeAmtNumberOfEachCoinType = [] + numberOfEachCoinType
                    smallerChangeAmtNumberOfEachCoinType[index] += 1
                    solutionFound, bestFewestCoins, bestNumberOfEachCoinType = backtrack(smallerChangeAmt, smallerChangeAmtNumberOfEachCoinType,numberOfCoinsSoFar + 1, solutionFound, bestFewestCoins, bestNumberOfEachCoinType)
                    
        return solutionFound, bestFewestCoins, bestNumberOfEachCoinType
    # end def backtrack
    
    def promising(changeAmt, numberOfCoinsReturned, solutionFound, bestFewestCoins):
        if changeAmt < 0:
            return False
        elif changeAmt == 0:
            return True
        else: # changeAmt > 0
            if solutionFound and numberOfCoinsReturned+1 >= bestFewestCoins:
                return False
            else:
                return True
            
    # set-up initial "current state" information
    numberOfEachCoinType = []
    numberOfCoinsSoFar = 0
    solutionFound = False
    bestFewestCoins = -1
    bestNumberOfEachCoinType = None
    
    numberOfEachCoinType = []
    for coin in coinTypes:
        numberOfEachCoinType.append(0)
    numberOfCoinsSoFar = 0
    solutionFound = False
    bestFewestCoins = -1
    bestNumberOfEachCoinType = None

    solutionFound, bestFewestCoins, bestNumberOfEachCoinType = backtrack(changeAmt, numberOfEachCoinType, numberOfCoinsSoFar, solutionFound, bestFewestCoins, bestNumberOfEachCoinType)
    return bestFewestCoins, bestNumberOfEachCoinType

main()
print ("Number of Backtracking Nodes:", backtrackingNodes)
