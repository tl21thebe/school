#include <iostream>
#include "PSO.h"
#include "SwarmGenerator.h"
#include "Function.h"
#include "Particle.h"
#include "Vector.h"
using namespace std;


int main() {
    // Generate initial swarm data
    /*SwarmGenerationProperties props;
    defaultSettings(props);
    string swarmData = generateSwarm(props, 12345L);
    toFile("swarm.txt", swarmData);*/

    // Initialize PSO with the generated data
    PSO pso("studentExample.txt");

    // Create a dummy Function object for evaluation
    Function dummyFunction;

    cout << "Population" << endl;
    for (int i = 0; i < pso.getNumberOfParticles(); ++i) {
        Particle* p = pso.getParticle(i);
        cout << "Particle " << i << ": P: " << p->getPosition().toString()
                  << "\tV: " << p->getVelocity().toString() << endl;
    }

    cout << "Manual Loop" << endl;
    for (int gen = 0; gen < 20; ++gen) {
        cout << "Generation " << gen << endl;
        const Particle& best = pso.run(dummyFunction);
        for (int i = 0; i < pso.getNumberOfParticles(); ++i) {
            Particle* p = pso.getParticle(i);
            cout << "\tParticle " << i << ": P: " << p->getPosition().toString()
                      << "\tV: " << p->getVelocity().toString() << endl;
        }
        cout << "Best particle: P: " << best.getPosition().toString()
                  << "\tV: " << best.getVelocity().toString() << endl;
        cout << endl;
    }
    for(int gen = 0; gen < 20; ++gen){
        const Particle& best = pso.run(dummyFunction);
        cout << "Generation " << gen << " best Particle: P : " << best.getPosition().toString()<< "\tV: " << best.getVelocity().toString() << endl;
    }
    return 0;
};
